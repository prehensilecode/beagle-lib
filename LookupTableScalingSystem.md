Constants for single precision:
```
    public static final int SCALING_FACTOR_COUNT = 254; // -126, 127
    public static final int SCALING_FACTOR_OFFSET = 126; // the zero point
    private static final int SCALING_EXPONENT_THRESHOLD = 20;
```

The actual scaling factors and their logs are pre-calculated for these exponents:
```
        int exponent = -126;
        for (int i = 0; i < SCALING_FACTOR_COUNT; i++) {
            scalingFactors[i] = Math.pow(2.0, exponent);
            logScalingFactors[i] = Math.log(scalingFactors[i]);
            exponent ++;
        }
```

When calculating the partial likelihoods the absolute value of their exponents is bit-wise ORed into an variable:
```
     exponent |= Math.abs(Math.getExponent(x));
```

After calculating the partial likelihoods for a node, this variable is tested to see if it is greater than `SCALING_EXPONENT_THRESHOLD` in which case a rescaling is triggered for that set of partials.

```
    private void rescalePartials(final int bufferIndex) {

        double[] partials = this.partials[bufferIndex];
        int[] counts = scalingFactorCounts[bufferIndex];

        int u = 0;
        for (int l = 0; l < categoryCount; l++) {

            for (int k = 0; k < patternCount; k++) {

                double maxValue = partials[u];

                for (int i = 1; i < stateCount; i++) {

                    if (partials[u + i] > maxValue) {
                        maxValue = partials[u + i];
                    }
                }

                // find the exponent for the largest value
                int exponent = Math.getExponent(maxValue);
                if (exponent != 0) {
                    // invert and offset it to get the index of the appropriate scale factor
                    int index = SCALING_FACTOR_OFFSET - exponent;
                    double scalingFactor = scalingFactors[index];

                    // increment the count of how many times this factor has been used
                    counts[index] ++;

                    // do the rescaling
                    for (int i = 0; i < stateCount; i++) {
                        partials[u] *= scalingFactor;
                        u++;
                    }
                }
            }
        }
    }
```

Finally the log scale factors are subtracted from the log likelihood:
```
            int[] rootCounts = scalingFactorCounts[bufferIndices[0]];
            for (int i = 0; i < SCALING_FACTOR_COUNT; i++) {
                // we multiplied the scaling factors in so now subtract the logs
                outSumLogLikelihood[0] -= rootCounts[i] * logScalingFactors[i];
            }
```

A few other notes:
  * I don't accumulate the largest exponent in `updateStatesStates` as this is a 'cherry' subtending two tips and we can probably assume that there are no scaling issues on these.
  * The counts of scaling factors need to be accumulated from descendent nodes but this can be done in the calls that calculate the partial likelihoods. As the scaling count buffers 'shadow' the partial buffers, the same indices should be used. `updateStatesStates` simply zeros its counts as it isn't going to scale cherries, `updateStatesPartials` just copies the counts from the internal node and `updatePartialsPartials` adds the counts from the two nodes below.
  * The drawback of this scheme is that individual site likelihoods can't be calculated. If this is required then the count buffers would become arrays of indices, one for each site, indexing the exponent used (although this could be byte array saving 1/4 of the space over storing actual factors.