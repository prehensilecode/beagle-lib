## Prerequisites ##

You will need the following software to build beagle:
  * gcc
  * autotools (autoconf, automake, etc)
  * pkg-config
  * subversion
  * Nvidia Toolkit
  * Optional: Nvidia CUDA SDK

To use BEAGLE with NVidia graphics cards you will need to download and install the CUDA driver and tools from [http://www.nvidia.com/object/cuda\_get.html](http://www.nvidia.com/object/cuda_get.html).

## Build from the source repository ##

```
svn checkout http://beagle-lib.googlecode.com/svn/trunk/ beagle-lib-read-only
cd beagle-lib-read-only
./autogen.sh
./configure --prefix=$HOME
make install
```

## Using the installed beagle library ##

If you followed the instructions above, then beagle was installed to your home directory.  You'll need to tell other programs to find the beagle library in your home directory by setting the LD\_LIBRARY\_PATH environment variable:
```
export LD_LIBRARY_PATH=$HOME/lib:$LD_LIBRARY_PATH
```
Or if using tcsh:
```
setenv LD_LIBRARY_PATH $HOME/lib:$LD_LIBRARY_PATH
```
That command will need to be run every time you log in, so it's best to put it in a login script such as .bashrc or .profile or .cshrc, etc.

If you plan to build other applications that depend on beagle, you'll also need be sure beagle is in your pkg-config path:
```
export PKG_CONFIG_PATH=$HOME/lib/pkgconfig:$PKG_CONFIG_PATH
```
This too can be put in a login script.

## Notes on prerequisite software ##

The prerequisite software should be fairly easy to install.  On Mac OS X you'll need to install the Xcode Developer Tools, then build and install pkg-config from source.
On Ubuntu, the requisite software can be obtained via apt-get:
```
sudo apt-get install automake
sudo apt-get install pkg-config
```