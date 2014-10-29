Platforms Compatibility for Minko 3 BETA 1
==========================================

The platforms compatibility matrix provides the current state of support for each platform officially targeted by the Minko Framework. you can consult the [plugins compatibility matrix](Plugins_compatibility_matrix.md) to find out more about the plugins support for each platform.

Platforms officially targeted
-----------------------------

|                                                                         |                                | Premake configuration name       |
|-------------------------------------------------------------------------|--------------------------------|----------------------------------|
| align=left|![](images/Html5_min.png "fig:images/Html5_min.png") HTML5   | ![](checked.png "checked.png") | html5                            |
| align=left|![](winmini.png "fig:winmini.png") Windows                   | ![](checked.png "checked.png") | windows32\<br/\>windows64        |
| align=left|![](mac_min.png "fig:mac_min.png") OS X                      | ![](checked.png "checked.png") | osx64                            |
| align=left|![](linux_min.png "fig:linux_min.png") Linux                 | ![](checked.png "checked.png") | linux32\<br/\>linux64            |
| align=left|![](androidmini.png "fig:androidmini.png") Android           | ![](help_16.png "help_16.png") | N/A (expected for the beta 2...) |
| align=left|![](iso7mini.png "fig:iso7mini.png") iOS                     | ![](checked.png "checked.png") | ios                              |
| align=left|![](flashmini.png "fig:flashmini.png") Flash                 | ![](help_16.png "help_16.png") | N/A                              |
| align=left|![](Windows phone.png "fig:Windows phone.png") Windows Phone | ![](help_16.png "help_16.png") | N/A                              |

Target compatibility matrices
-----------------------------

For each platform, support may vary depending of the host version, the possible states for each host are :

-   ![](checked.png "fig:checked.png"): Fully supported
-   ![](warning.png "fig:warning.png"): Partially supported
-   ![](error.png "fig:error.png"): Not supported
-   ![](help_16.png "fig:help_16.png"): Not supported yet

### ![](images/Html5_min.png "fig:images/Html5_min.png") HTML5

Minko for HTML5 relies only on WebGL, the HTML5 standard API to create 3D web applications. For more details about WebGL availability, please consult the corresponding ["Can I use..." page](http://caniuse.com/#search=webgl).

| Host        | Support                                                                                                                     |
|-------------|-----------------------------------------------------------------------------------------------------------------------------|
| Chrome 20+  | ![](checked.png "checked.png")                                                                                              |
| Firefox 20+ | ![](checked.png "checked.png")                                                                                              |
| IE 6-10     | ![](error.png "fig:error.png") Not supported as those versions of Internet explorer do NOT support the WebGL fonctionality. |
| IE 11       | ![](warning.png "fig:warning.png") Some functionalities might not be fully supported                                        |
| Opera 18+   | ![](checked.png "checked.png")                                                                                              |

### ![](Winmini.png "fig:Winmini.png") Microsoft Windows

| Host          | Support                                                                                                                                                        |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Windows XP    | ![](error.png "fig:error.png") Windows XP cannot be targeted as the Visual Studio 2013 C++ compiler have ended support for this particular version of Windows. |
| Windows Vista | ![](checked.png "checked.png")                                                                                                                                 |
| Windows Seven | ![](checked.png "checked.png")                                                                                                                                 |
| Windows 8+    | ![](checked.png "checked.png")                                                                                                                                 |

### ![](mac_min.png "fig:mac_min.png") Apple OS X

| Host                 | Support                                                                                                                                                            |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 10.6 "Snow Leopard"  | ![](error.png "fig:error.png") Even if targeting MacOS 10.6 is technically feasible with some hacking, this version is no more supported by Apple Xcode toolchain. |
| 10.7 "Lion"          | ![](checked.png "checked.png")                                                                                                                                     |
| 10.8 "Mountain Lion" | ![](checked.png "checked.png")                                                                                                                                     |
| 10.9 "Mavericks"     | ![](checked.png "checked.png")                                                                                                                                     |

### ![](linux_min.png "fig:linux_min.png") GNU/Linux

| Host                       | Support                        |
|----------------------------|--------------------------------|
| X86 or X86\64 Kernel 2.6+ | ![](checked.png "checked.png") |
| ARM - kernel 2.6+          | ![](checked.png "checked.png") |

### ![](androidmini.png "fig:androidmini.png") Android

| Host         | Support                                                                         |
|--------------|---------------------------------------------------------------------------------|
| Android 2.5+ | ![](help_16.png "fig:help_16.png") We're working on it ! Expected for beta 2... |

### ![](iso7mini.png "fig:iso7mini.png") Apple iOS

| Host     | Support                        |
|----------|--------------------------------|
| iOS 4.0+ | ![](checked.png "checked.png") |

### ![](flashmini.png "fig:flashmini.png") Adobe Flash

| Host        | Support                                                 |
|-------------|---------------------------------------------------------|
| Flash 11.2+ | ![](help_16.png "fig:help_16.png") We're working on it! |

### ![](Windows phone.png "fig:Windows phone.png") Windows Phone

| Host               | Support                                                 |
|--------------------|---------------------------------------------------------|
| Windows Phone 8.1+ | ![](help_16.png "fig:help_16.png") We're working on it! |


