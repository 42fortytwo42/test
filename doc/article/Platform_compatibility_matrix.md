Platforms Compatibility for Minko 3 BETA 1
==========================================

The platforms compatibility matrix provides the current state of support for each platform officially targeted by the Minko Framework. you can consult the [plugins compatibility matrix](../Plugins_compatibility_matrix.md) to find out more about the plugins support for each platform.

Platforms officially targeted
-----------------------------

|                                                                                           |                                                  | Premake configuration name       |
|-------------------------------------------------------------------------------------------|--------------------------------------------------|----------------------------------|
| align=left|![](../image/Html5_min.png "fig:../image/Html5_min.png") HTML5                 | ![](../image/Checked.png "../image/Checked.png") | html5                            |
| align=left|![](../image/Winmini.png "fig:../image/Winmini.png") Windows                   | ![](../image/Checked.png "../image/Checked.png") | windows32<br/>windows64        |
| align=left|![](../image/Mac_min.png "fig:../image/Mac_min.png") OS X                      | ![](../image/Checked.png "../image/Checked.png") | osx64                            |
| align=left|![](../image/Linux_min.png "fig:../image/Linux_min.png") Linux                 | ![](../image/Checked.png "../image/Checked.png") | linux32<br/>linux64            |
| align=left|![](../image/Androidmini.png "fig:../image/Androidmini.png") Android           | ![](../image/Help_16.png "../image/Help_16.png") | N/A (expected for the beta 2...) |
| align=left|![](../image/Iso7mini.png "fig:../image/Iso7mini.png") iOS                     | ![](../image/Checked.png "../image/Checked.png") | ios                              |
| align=left|![](../image/Flashmini.png "fig:../image/Flashmini.png") Flash                 | ![](../image/Help_16.png "../image/Help_16.png") | N/A                              |
| align=left|![](../image/Windows_phone.png "fig:../image/Windows_phone.png") Windows Phone | ![](../image/Help_16.png "../image/Help_16.png") | N/A                              |

Target compatibility matrices
-----------------------------

For each platform, support may vary depending of the host version, the possible states for each host are :

-   ![](../image/Checked.png "fig:../image/Checked.png"): Fully supported
-   ![](../image/Warning.png "fig:../image/Warning.png"): Partially supported
-   ![](../image/Error.png "fig:../image/Error.png"): Not supported
-   ![](../image/Help_16.png "fig:../image/Help_16.png"): Not supported yet

### ![](../image/Html5_min.png "fig:../image/Html5_min.png") HTML5

Minko for HTML5 relies only on WebGL, the HTML5 standard API to create 3D web applications. For more details about WebGL availability, please consult the corresponding [<http://caniuse.com/>#search=webgl "Can I use..." page].

| Host        | Support                                                                                                                                       |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| Chrome 20+  | ![](../image/Checked.png "../image/Checked.png")                                                                                              |
| Firefox 20+ | ![](../image/Checked.png "../image/Checked.png")                                                                                              |
| IE 6-10     | ![](../image/Error.png "fig:../image/Error.png") Not supported as those versions of Internet explorer do NOT support the WebGL fonctionality. |
| IE 11       | ![](../image/Warning.png "fig:../image/Warning.png") Some functionalities might not be fully supported                                        |
| Opera 18+   | ![](../image/Checked.png "../image/Checked.png")                                                                                              |

### ![](../image/Winmini.png "fig:../image/Winmini.png") Microsoft Windows

| Host          | Support                                                                                                                                                                          |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Windows XP    | ![](../image/Error.png "fig:../image/Error.png") Windows XP cannot be targeted as the Visual Studio 2013 C++ compiler have ended support for this particular version of Windows. |
| Windows Vista | ![](../image/Checked.png "../image/Checked.png")                                                                                                                                 |
| Windows Seven | ![](../image/Checked.png "../image/Checked.png")                                                                                                                                 |
| Windows 8+    | ![](../image/Checked.png "../image/Checked.png")                                                                                                                                 |

### ![](../image/Mac_min.png "fig:../image/Mac_min.png") Apple OS X

| Host                 | Support                                                                                                                                                                              |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 10.6 "Snow Leopard"  | ![](../image/Error.png "fig:../image/Error.png") Even if targeting MacOS 10.6 is technically feasible with some hacking, this version is no more supported by Apple Xcode toolchain. |
| 10.7 "Lion"          | ![](../image/Checked.png "../image/Checked.png")                                                                                                                                     |
| 10.8 "Mountain Lion" | ![](../image/Checked.png "../image/Checked.png")                                                                                                                                     |
| 10.9 "Mavericks"     | ![](../image/Checked.png "../image/Checked.png")                                                                                                                                     |

### ![](../image/Linux_min.png "fig:../image/Linux_min.png") GNU/Linux

| Host                       | Support                                          |
|----------------------------|--------------------------------------------------|
| X86 or X86_64 Kernel 2.6+ | ![](../image/Checked.png "../image/Checked.png") |
| ARM - kernel 2.6+          | ![](../image/Checked.png "../image/Checked.png") |

### ![](../image/Androidmini.png "fig:../image/Androidmini.png") Android

| Host         | Support                                                                                           |
|--------------|---------------------------------------------------------------------------------------------------|
| Android 2.5+ | ![](../image/Help_16.png "fig:../image/Help_16.png") We're working on it ! Expected for beta 2... |

### ![](../image/Iso7mini.png "fig:../image/Iso7mini.png") Apple iOS

| Host     | Support                                          |
|----------|--------------------------------------------------|
| iOS 4.0+ | ![](../image/Checked.png "../image/Checked.png") |

### ![](../image/Flashmini.png "fig:../image/Flashmini.png") Adobe Flash

| Host        | Support                                                                   |
|-------------|---------------------------------------------------------------------------|
| Flash 11.2+ | ![](../image/Help_16.png "fig:../image/Help_16.png") We're working on it! |

### ![](../image/Windows_phone.png "fig:../image/Windows_phone.png") Windows Phone

| Host               | Support                                                                   |
|--------------------|---------------------------------------------------------------------------|
| Windows Phone 8.1+ | ![](../image/Help_16.png "fig:../image/Help_16.png") We're working on it! |


