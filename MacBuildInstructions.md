## Installing BEAGLE on Mac OS X ##
BEAGLE is a high-performance library that can perform the core calculations at the heart of most Bayesian and Maximum Likelihood phylogenetics package. It can make use of highly-parallel processors such as those in 3D graphics boards found in many PCs.

To install it on Mac OS X you will need to install Apple's developer tools. These may be on your Mac OS X install disk as an optional installation (look for 'Xcode'). You can also download them from [http://developer.apple.com](http://developer.apple.com).

To use BEAGLE with NVIDIA graphics cards you will need to download and install the CUDA driver and tools from [http://www.nvidia.com/object/cuda\_get.html](http://www.nvidia.com/object/cuda_get.html). Select "Mac OS" as the Operating System and then select the 'Developer Drivers for MacOS' package. You will also need to download and install the 'CUDA Toolkit' package.

Next you will need to download and install BEAGLE. Open 'Terminal.app' and type:

```
svn checkout http://beagle-lib.googlecode.com/svn/trunk/ beagle-lib
```

This will download BEAGLE into a folder called 'beagle-lib'. Type:

```
cd beagle-lib
./autogen.sh
./configure
make
sudo make install
```

You will have to type your admin password in for the last of these commands.

Finally to check that the installation worked and that your NVIDIA card is working type:

```
make check
```

This will run a suit of test programs using the BEAGLE library.