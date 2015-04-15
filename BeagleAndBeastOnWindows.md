# Introduction #

This is still a draft document.  Any instructions found here may not work at all.  You've been warned!
Current builds of libhmsbeagle require the Nvidia CUDA hardware driver to be installed.  Thanks to Chris Drummond for suggestions and testing.

# Details #

Step 1.  Download and use the beagle windows installer, **reboot when done**.  Installer currently available from:
http://edhar.genomecenter.ucdavis.edu/~koadman/libhmsbeagle-20100716.msi

Step 2.  Get a current beast.
```
svn co http://beast-mcmc.googlecode.com/svn/trunk/ beast-mcmc
```

Step 3.  Build beast
```
cd beast-mcmc
ant
```

Step 4.  Run beast
```
java -Xmx500m -cp build\dist\beast.jar;%LIBHMSBEAGLE-1.0%\beagle.jar -Djava.library.path=%LIBHMSBEAGLE-1.0% dr.app.beast.BeastMain -beagle -beagle_GPU -beagle_order 1,1,2,2,0,0 name.of.your.input.file.xml
```


# Building from source in Visual Studio #

The following software prerequisites must be installed prior to building libhmsbeagle on windows:

  * A 64-bit Windows OS (XP or later)
  * Visual Studio Professional 2008 (express edition will not work)
  * Java Development Kit 1.5 or later
  * Nvidia CUDA 2.3, 64-bit (3.0 has not been tested, not by me anyway)
  * The video card driver is required to use the library, but not to build it

Step 1. Checkout the source code repository:
```
svn co http://beagle-lib.googlecode.com/svn/trunk/ beagle-lib
```

Step 2. Open the Visual Studio 2008 project:
  * It's located at project\beagle-vs\libhmsbeagle\_vc90.sln

Step 3. Set the desired configuration (e.g. "Release" and X64)

Step 4. Right-click on the installer project (at the left hand side in the project explorer) and select "build"

Step 5. The installer will be located in project\beagle-vs\beagleinstaller\Release, assuming a release build.  Note that if error messages appear that the build system was unable to find Java, then you must build from the command line with build\_installer.bat.  See below.

**Alternate approach:**  Edit the file project\beagle-vs\build\_installer.bat to point to the Visual Studio and ant installations, and run it from within a command prompt.  Skip steps 2-4.