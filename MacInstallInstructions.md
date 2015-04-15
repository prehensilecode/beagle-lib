### Installing BEAGLE on Mac OS X ###
The easiest way to install BEAGLE is to use the binary installer.

**Step 1.** Download and run the binary installer:
  * [BEAGLE v2.1.2 for OS X 10.6 and later](https://www.dropbox.com/s/we3mryobwqwmbgg/BEAGLE-2.1.2.pkg)

**Step 2. (optional)** If you have OS X v10.6 or later and wish to use BEAGLE with an NVIDIA GPU via CUDA, please download and install the latest NVIDIA CUDA drivers for Mac OS from nvidia.com:
  * [NVIDIA CUDA drivers for Mac](http://www.nvidia.com/object/mac-driver-archive.html)

After the installations above are complete you will be ready to use BEAGLE with compatible applications such as BEAST, MrBayes, and GARLI.

For instructions on how to use BEAGLE with BEAST please refer to [Using BEAGLE with BEAST](http://beast.bio.ed.ac.uk/BEAGLE)


---


#### Installing from source ####
If you have problems with the binary installer or wish to use the very latest SVN revision you may build BEAGLE from source.

**Step 1.** You will need to install Xcode, which includes Apple's developer tools. You can download Xcode from the [Mac App Store](https://itunes.apple.com/us/app/xcode/id497799835).

**Step 2.** Next, you need to obtain the following software packages: _autoconf_, _automake_, and _libtool_. The easiest way to install these is with the [Homebrew package manager](http://brew.sh). Open 'Terminal.app' and paste the installation command from the [Homebrew website](http://brew.sh) (you will find it at the bottom of the page, under _Install Homebrew_). Next enter the following to install the required packages:
```
brew install libtool autoconf automake
```

**Step 3. (optional)** To use BEAGLE with CUDA for NVIDIA graphics cards you will need to download and install the [CUDA Toolkit for Mac OS X](https://developer.nvidia.com/cuda-downloads).

**Step 4.** Next you will need to download the BEAGLE source code. In the Terminal, type:
```
svn checkout http://beagle-lib.googlecode.com/svn/trunk/ beagle-lib
```
This will download the BEAGLE source into a folder called 'beagle-lib'.

**Step 5.** The next step is to compile the BEAGLE library. Type:
```
cd beagle-lib
./autogen.sh
./configure
make
sudo make install
```
You will have to enter your user password for the last of these commands.

**Step 6.** Finally, to check that the installation worked type:
```
make check
```
This will run a suite of test programs using the BEAGLE library.