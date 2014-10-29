Platforms Compatibility for Minko 3 BETA 1
==========================================

The platforms compatibility matrix provides the current state of support for each platform officially targeted by the Minko Framework. you can consult the [plugins compatibility matrix](Plugins_compatibility_matrix.md) to find out more about the plugins support for each platform.

Platforms officially targeted
-----------------------------

|                                                                                       |                                              | Premake configuration name       |
|---------------------------------------------------------------------------------------|----------------------------------------------|----------------------------------|
| align=left|![](images/Html5_min.png "fig:images/Html5_min.png") HTML5                 | ![](images/Checked.png "images/Checked.png") | html5                            |
| align=left|![](images/Winmini.png "fig:images/Winmini.png") Windows                   | ![](images/Checked.png "images/Checked.png") | windows32\<br/\>windows64        |
| align=left|![](images/Mac_min.png "fig:images/Mac_min.png") OS X                      | ![](images/Checked.png "images/Checked.png") | osx64                            |
| align=left|![](images/Linux_min.png "fig:images/Linux_min.png") Linux                 | ![](images/Checked.png "images/Checked.png") | linux32\<br/\>linux64            |
| align=left|![](images/Androidmini.png "fig:images/Androidmini.png") Android           | ![](images/Help_16.png "images/Help_16.png") | N/A (expected for the beta 2...) |
| align=left|![](images/Iso7mini.png "fig:images/Iso7mini.png") iOS                     | ![](images/Checked.png "images/Checked.png") | ios                              |
| align=left|![](images/Flashmini.png "fig:images/Flashmini.png") Flash                 | ![](images/Help_16.png "images/Help_16.png") | N/A                              |
| align=left|![](images/Windows_phone.png "fig:images/Windows_phone.png") Windows Phone | ![](images/Help_16.png "images/Help_16.png") | N/A                              |

Target compatibility matrices
-----------------------------

For each platform, support may vary depending of the host version, the possible states for each host are :

-   ![](images/Checked.png "fig:images/Checked.png"): Fully supported
-   ![](images/Warning.png "fig:images/Warning.png"): Partially supported
-   ![](images/Error.png "fig:images/Error.png"): Not supported
-   ![](images/Help_16.png "fig:images/Help_16.png"): Not supported yet

### ![](images/Html5_min.png "fig:images/Html5_min.png") HTML5

Minko for HTML5 relies only on WebGL, the HTML5 standard API to create 3D web applications. For more details about WebGL availability, please consult the corresponding ["Can I use..." page](http://caniuse.com/#search=webgl).

| Host        | Support                                                                                                                                   |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| Chrome 20+  | ![](images/Checked.png "images/Checked.png")                                                                                              |
| Firefox 20+ | ![](images/Checked.png "images/Checked.png")                                                                                              |
| IE 6-10     | ![](images/Error.png "fig:images/Error.png") Not supported as those versions of Internet explorer do NOT support the WebGL fonctionality. |
| IE 11       | ![](images/Warning.png "fig:images/Warning.png") Some functionalities might not be fully supported                                        |
| Opera 18+   | ![](images/Checked.png "images/Checked.png")                                                                                              |

### ![](images/Winmini.png "fig:images/Winmini.png") Microsoft Windows

| Host          | Support                                                                                                                                                                      |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Windows XP    | ![](images/Error.png "fig:images/Error.png") Windows XP cannot be targeted as the Visual Studio 2013 C++ compiler have ended support for this particular version of Windows. |
| Windows Vista | ![](images/Checked.png "images/Checked.png")                                                                                                                                 |
| Windows Seven | ![](images/Checked.png "images/Checked.png")                                                                                                                                 |
| Windows 8+    | ![](images/Checked.png "images/Checked.png")                                                                                                                                 |

### ![](images/Mac_min.png "fig:images/Mac_min.png") Apple OS X

| Host                 | Support                                                                                                                                                                          |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 10.6 "Snow Leopard"  | ![](images/Error.png "fig:images/Error.png") Even if targeting MacOS 10.6 is technically feasible with some hacking, this version is no more supported by Apple Xcode toolchain. |
| 10.7 "Lion"          | ![](images/Checked.png "images/Checked.png")                                                                                                                                     |
| 10.8 "Mountain Lion" | ![](images/Checked.png "images/Checked.png")                                                                                                                                     |
| 10.9 "Mavericks"     | ![](images/Checked.png "images/Checked.png")                                                                                                                                     |

### ![](images/Linux_min.png "fig:images/Linux_min.png") GNU/Linux

| Host                       | Support                                      |
|----------------------------|----------------------------------------------|
| X86 or X86\64 Kernel 2.6+ | ![](images/Checked.png "images/Checked.png") |
| ARM - kernel 2.6+          | ![](images/Checked.png "images/Checked.png") |

### ![](images/Androidmini.png "fig:images/Androidmini.png") Android

| Host         | Support                                                                                       |
|--------------|-----------------------------------------------------------------------------------------------|
| Android 2.5+ | ![](images/Help_16.png "fig:images/Help_16.png") We're working on it ! Expected for beta 2... |

### ![](images/Iso7mini.png "fig:images/Iso7mini.png") Apple iOS

| Host     | Support                                      |
|----------|----------------------------------------------|
| iOS 4.0+ | ![](images/Checked.png "images/Checked.png") |

### ![](images/Flashmini.png "fig:images/Flashmini.png") Adobe Flash

| Host        | Support                                                               |
|-------------|-----------------------------------------------------------------------|
| Flash 11.2+ | ![](images/Help_16.png "fig:images/Help_16.png") We're working on it! |

### ![](images/Windows_phone.png "fig:images/Windows_phone.png") Windows Phone

| Host               | Support                                                               |
|--------------------|-----------------------------------------------------------------------|
| Windows Phone 8.1+ | ![](images/Help_16.png "fig:images/Help_16.png") We're working on it! |


