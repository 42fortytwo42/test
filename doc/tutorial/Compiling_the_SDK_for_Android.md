This tutorial will guide through the few steps to compile the Minko SDK **for Android** using the command line. Compiling the SDK for Android should work on Windows, OS X, Linux.

To target Android, the Android [SDK](http://developer.android.com/sdk/index.html) and [NDK](https://developer.android.com/tools/sdk/ndk/index.html) must be installed. Both are free and available on all supported platforms. However, on Windows, **Cygwin** is an additional requirement. Though you can follow Google's [instructions](http://www.kandroid.org/ndk/docs/STANDALONE-TOOLCHAIN.html) regarding the installation of the toolchain, all necessary steps will be detailed here.

Step 1: Get the sources
-----------------------

Make sure you have the source code of Minko on your filesystem. You can get them from our repository: [Installing the Minko SDK sources](Installing_the_SDK_sources.md#step-1-install-a-git-client).

Step 2: Installing the Android environment
------------------------------------------

### Installing a Unix environment (Windows only)

**On Linux and OS X, you should be fine with your default environment. Please skip this step.**

On Windows however, [Cygwin](http://cygwin.com/) 1.7+ must be installed. Cygwin is a Unix environment for Windows which is required to run the NDK. On other platforms, you should be fine with your default environment, so skip this part.

Once you have downloaded the installer, run it. Choose **Install from Internet**, click **Next**. You should be fine with all the default options. After you have selected a mirror and clicked **Next**, Cygwin will download and present to you the list of available packages.

By default, only the base packages are installed. We, however, need the development packages. Rather than picking the packages we think we need, and then struggling with missing dependencies and other typical Unix nightmares, I suggest that we install the entire **Devel** branch. Click (once) on the word **Default** next to the root Devel node and wait few seconds while the setup hangs.

![](../../doc/image/Cygwin_setup_packages.jpg "../../doc/image/Cygwin_setup_packages.jpg")

When it is back, you will see that **Default** changes to **Install** for the **Devel** node. Install and wait. This may take a while.

### Installing the Android SDK

-   Define the environment variable `ANDROID` pointing to the following directory:
    -   Windows: `C:\android`
    -   OS X / Linux: `/opt/android`
-   Download the latest [ADT](http://developer.android.com/sdk/index.html) bundle
-   Extract the archive to the `${ANDROID}` directory

### Installing the Android NDK

-   Download the latest [Android NDK](https://developer.android.com/tools/sdk/ndk/index.html) package
-   Extract the archive to `${ANDROID}/NDK`
-   Run the following script:
    -   Windows: `tool\win\script\install_jni.bat`
    -   Linux: `tool/lin/script/install_jni.sh`
    -   OS X: `tool/mac/script/install_jni.sh`

### Installing ANT

-   Windows: decompress the [ANT binary archive](https://www.apache.org/dist/ant/binaries/) in the `${ANDROID}/ant` directory and add `${ANDROID}/ant/bin` to your `Path` environment variable.
-   OS X: use the `brew` package manager using the `brew install ant` command
-   Linux: `apt-get install ant`

The final folder hierarchy should be as follow:

```
 ${ANDROID}

 /ant
 /build-tools
 /extras
 /ndk
   /android-ndk-r${VERSION}
 /platforms
 /platform-tools
 /toolchains
 /tools

```


Node: the `${ANDROID}/ant` directory should exist only on Windows.

Step 3: Generating the JNI solution
-----------------------------------

Minko's SDK uses premake5, which is embed in the SDK, for its build system. The Native Development Kit for Android uses Makefiles, so we can use the default Cygwin GNU make.

To do this, open a command line prompt in the root directory of the SDK and run:

-   Windows: `tool\win\script\solution_gmake.bat`
-   Linux: `tool/lin/script/solution_gmake.sh`
-   OS X: `tool/mac/script/solution_gmake.sh`

Step 4: Compile the SDK
-----------------------

Now, you should have a bunch of Makefiles. You can build the solution using the following command line:

```bash
$ make config=android_release 
```


If you want to leverage multicore processors, you can use the following command line (replace '4' by your actual number of cores):

```bash
$ make -j 4 config=android_release 
```


It should speed up the compilation process significantly.

Step 5 (optional): Re-compile SDL2
----------------------------------

If you get undefined reference errors for SDL2 functions at linkage when building the SDK's examples/tutorials, it means you might have to rebuild SDL2 for your NDK/platform. By default, Minko builds for **ARMv7**. If you need to support another architecture, you will have to rebuild SDL2.

To do this, regenerate the solution with the `--rebuild-sdl` option:

-   Linux: `tool/lin/script/premake5.sh gmake --rebuild-sdl`
-   OS X: `tool/mac/script/premake5.sh gmake --rebuild-sdl`

Then try the step 4 again. Your solution should contain a new SDL2 project that will be built using your version of the Android NDK and you should not get any linkage error.

Step 6: Enjoy!
--------------

Now use your SDK to [Create a new application](../tutorial/Create_a_new_application.md).

