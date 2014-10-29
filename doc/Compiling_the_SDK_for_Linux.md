**The following tutorial assumes you are using a supported platform and that your environment is already set up to build Minko applications.**

Step 1: Get the SDK sources
---------------------------

Make sure you have the source code of Minko on your filesystem. You can get them from our repository: [Installing the Minko SDK sources](Installing the SDK (Git)).

Step 2: Install the dependencies
--------------------------------

If you've never build a Minko application or the Minko SDK for Linux before, follow the [step 1 of the Targeting Linux tutorial](Targeting_Linux#Step_1:_Installing_the_toolchain).

Step 3: Generate the solution
-----------------------------

Minko uses Premake for its build system. Premake is a nice solution to have a cross-platform build system that can work across multiple IDEs such as Xcode, Visual Studio and even GNU Make. In order to build the SDK, we will generate a solution for `gmake`. We need to use a terminal to generate a `Makefile`-compatible solution:


```
 cd ${MINKO\HOME} tool/lin/script/premake5.sh gmake 
```


If we want to select your compiler, we can pass the `cc` option. Supported values are `gcc` and `clang`:


```
 tool/lin/script/premake5.sh --cc=clang gmake 
```


To learn more about premake commands, run:


```
 tool/lin/script/premake5.sh --help 
```


![](images/Minko linux premake gmake.jpg "images/Minko linux premake gmake.jpg")

The list of the projects may vary according to the actual version of the SDK. What's important is to make sure that you have a `Makefile` at the root of the SDK and in each project directory.

Step 4: Compile the SDK
-----------------------

From the root directory of the SDK, simply run `make` with a valid configuration for your platform:


```
 make config=linux32\release 
```


Valid configurations for `gmake` are:

-   `linux32\release`
-   `linux32\debug`
-   `linux64\release`
-   `linux64\debug`

To leverage multi-core systems, you can also use `make -j`. The following example will use 4 cores and will compile the SDK much faster as a result:


```
 make -j4 config=linux32\release verbose=1 
```


Step 5: Package
---------------

The SDK is now built, but you might want to share or copy it so you don't have to deal with the sources again. We use a script to produce a distributable SDK.


```
 tool/lin/scripts/premake5.sh dist 
```


This should produce an archive in the root of the SDK which contains all the binaries built for your platform.

Step 6: Enjoy!
--------------

Now use your SDK to [Create a new application](Create_a_new_application.md).
