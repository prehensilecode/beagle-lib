## Introduction ##

This page contains basic instructions on how to build and link against beagle.  It doesn't discuss how to use the beagle API, rather we're going to assume you've already written a C or C++ program that uses beagle.  We'll assume your program's source code is in a file called my\_fly\_beagle\_app.cpp.  For examples on how the beagle API might be used, check out the examples directory in the beagle source tree.

### Building your app ###

The beagle library uses pkg-config to provide compiler flags for compiling and link against beagle.  In order to use pkg-config, the hmsbeagle-1.0.pc file must be in a directory listed in your PKG\_CONFIG\_PATH environment variable, or be in one of the default pkg-config directories.  Once that's done, building your app is as simple as running the following command:
```
g++ -o my_fly_beagle_app my_fly_beagle_app.cpp `pkg-config --cflags --libs hmsbeagle-1`
```

Note the use of backticks, that's shell code that runs the command in backticks and pastes the output into the command-line.  The pkg-config command requests the compiler and linker flags to link against the hmsbeagle library, API version 1.0.  If you'd like to link against another installed version of the API, change the version number appropriately.

That's all!

## A slightly more complex example ##

If writing a new beagle app from scratch, we recommend starting from the standalone example inside the beagle source tree.  The advantage of using this example is that it comes with an autotools build system already set up to use beagle.  It can be obtained with the following command:
```
svn export https://beagle-lib.googlecode.com/svn/trunk/examples/standalone/hellobeagle hellobeagle 
```

At that point, one can start editing the src/hello.cpp file to accomplish the appropriate phylogenetic likelihood calculation task.