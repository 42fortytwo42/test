You can add 4 different type of lights in your scene for this, open the right click menu on the scene tree where you want to add your light, and go in the `Add Light` submenu.

Ambient Light
=============

An ambient light will affect all objects in the scene and light them equally on all surface.

-   `Color`: changes the light color
-   `Ambient`: changes the intensity of the light. All materials can accentuate this intensity with the `Ambient Multiply` parameter.
-   `Emission`: sets the emission mask for the light. Any material with a layer enabled in its `reception` mask will be affected by the light if this same layer is enabled in the `emission` mask

 

-   Ambient = 0

![](images/Ambient0.png "images/Ambient0.png")

-   Ambient = 0.5

![](images/Ambient0.5.png "images/Ambient0.5.png")

-   Ambient = 1

![](images/Ambient1.png "images/Ambient1.png")

A scene with a single `ambient light` with white color and `ambient` set to 1 will look just like it would in `Basic` rendering mode.

Directional Light
=================

Directional lights, as their name suggest, light the nodes from your scene uniformly, in a defined direction.

Transform parameters
--------------------

In the `transform` section, you can see two parameters: `position` and `target position`. The direction of the light will go from the `position` point to the `target position`.

On the scene, the arrow will indicate the direction in which your light points. The position will have no influence on the way the scene is lighted, it will only change how shadows are cast. See the `shadow` section below for more information.

Light parameters
----------------

-   `Color`: changes the light color.
-   `Diffuse`: changes the intensity of the light. All materials can accentuate this intensity with the `Diffuse Multiplier` parameter.
-   `Shininess`: this will affect the spread of the specular spot. A bigger value will result in a smaller spot.
-   `Specular`: this will affect the intensity and radius of the light specular spot. A bigger value will result in a bigger size and intensity.

 

-   Diffuse = 0.1

![](images/Dirdiffuse0.1.png "images/Dirdiffuse0.1.png")

-   Diffuse = 0.3

![](images/Dirdiffuse0.3.png "images/Dirdiffuse0.3.png")

-   Diffuse = 0.6

![](images/Dirdiffuse0.6.png "images/Dirdiffuse0.6.png")

-   Shininess = 1024

![](images/Dirshininess1024.png "images/Dirshininess1024.png")

-   Shininess = 128

![](images/Dirshininess128.png "images/Dirshininess128.png")

-   Shininess = 40

![](images/Dirshininess40.png "images/Dirshininess40.png")

-   Specular = 0

![](images/Dirspecular0.png "images/Dirspecular0.png")

-   Specular = 0.3

![](images/Dirspecular0.3.png "images/Dirspecular0.3.png")

-   Specular = 0.8

![](images/Dirspecular0.8.png "images/Dirspecular0.8.png")

-   Specular = 2

![](images/Dirspecular2.png "images/Dirspecular2.png")

Shadows
-------

### Common Parameters

-   `Map Size`: size of the map used to draw shadows to. A bigger size will result in better, cleaner shadows, but a smaller size will be better for performance.
-   `Quality`: changes the way shadows are computed. Higher quality could impact on the performances.
-   `Map width`: width on which the shadows will be computed. Will be represented on screen by the light frustum. The position of this frustum will depend on the light `position`.
-   `Z-far`: maximum distance on which the shadows will be produced. Will be represented on screen by the light frustum.

 

-   Small `map width`: the shadows of the cube and torus are cut.

![](images/Dirshadowsmallfrustum.png "images/Dirshadowsmallfrustum.png")

-   Larger `map width`: the shadows of the cube and torus are fully visible.

![](images/Dirshadowlargerfrustum.png "images/Dirshadowlargerfrustum.png")

-   `Map size` = `64` `Quality` = Hard

![](images/Dirshadowhard64.png "images/Dirshadowhard64.png")

-   `Map size` = `512` `Quality` = Medium

![](images/Dirshadowmedium512.png "images/Dirshadowmedium512.png")

### Shadow mapping types

Minko provides two different shadow types.

-   `ESM`: exponential shadow mapping.
-   `PCF `: percentage-closer shadow mapping.

#### ESM

The ESM filters the shadow map by approximating the shadow test with an exponential function.

-   `Exponential factor`: a bigger value will give a better approximation

`ESM` works better with smaller `Z-far` and `Map width`.

-   `Exponential factor` = `1.5`, the two cube shadows have a slightly different color

![](images/Esmexp1.5.png "images/Esmexp1.5.png")

-   `Exponential factor` = `10`, the two cube shadows have the same color and blend in an uniform shadow

![](images/Esmexp10.png "images/Esmexp10.png")

#### PCF

`PCF` will filter the shadow map by calculating how far from the light the shadow is, producing sharper edges closer to the light and smoother ones further from the light.

-   `Bias`
-   `Spread`: how much the shadow will spread when it is far from the light

 

-   `Spread` = `0`, the shadow edges are sharp.

![](images/Pcfspread.png "images/Pcfspread.png")

-   `Spread` = `0`, the shadow edges are smoothed.

![](images/Pcfspread15.png "images/Pcfspread15.png")

Spot Light
==========

The light from a `spot light` originates from a point and is diffused in a cone.

Transform properties
--------------------

-   `Position`: position from which the `spot light` will emit.
-   `Target Position`: point to which the cone of the `spot light` will point.

Light properties
----------------

-   `Color</color>: changes the light color.
-   `Attenuation Distance`: distance at which the light intensity will fade out.
-   `Inner radius`, `Outer radius`: the `outer radius` gives the radius of the cone, the light will be more intense inside of the `inner radius` and will fade from the `inner radius` to the `outer radius`.
-   `Diffuse`: changes the intensity of the light. All materials can accentuate this intensity with the `Diffuse Multiplier` parameter.
-   `Shininess`: this will affect the spread of the specular spot. A bigger value will result in a smaller spot.
-   `Specular`: this will affect the intensity and radius of the light specular spot. A bigger value will result in a bigger size and intensity.

For `Shininess` and `Specular` examples, see above in the `Directional Light` section.

-   `Diffuse` = `0.5`

![](images/Spotdif0.5.png "images/Spotdif0.5.png")

-   `Diffuse` = `1`

![](images/Spotdif1.png "images/Spotdif1.png")

-   `Diffuse` = `5`

![](images/Spotdif5.png "images/Spotdif5.png")

-   Small `outer radius` and `inner radius`

![](images/Spotsmallradius.png "images/Spotsmallradius.png")

-   Bigger `outer radius`

![](images/Spotmediumradius.png "images/Spotmediumradius.png")

-   Bigger `outer radius` and `inner radius` close to the `outer radius`

![](images/Spotbigradius.png "images/Spotbigradius.png")

-   Small `Attenuation distance`

![](images/Spotsmallattenuation.png "images/Spotsmallattenuation.png")

-   Medium `Attenuation distance`

![](images/Spotmediumattenuation.png "images/Spotmediumattenuation.png")

-   Larger `Attenuation distance`

![](images/Spotbigattenuation.png "images/Spotbigattenuation.png")

Point Light
===========

Point lights send light in all directions.

Transform properties
--------------------

-   `Position`: position of the light source.

Light properties
----------------

-   `Color`: changes the light color.
-   `Attenuation Distance`: distance at which the light intensity will fade out.
-   `Diffuse`: changes the intensity of the light. All materials can accentuate this intensity with the `Diffuse Multiplier` parameter.
-   `Shininess`: this will affect the spread of the specular spot. A bigger value will result in a smaller spot.
-   `Specular`: this will affect the intensity and radius of the light specular spot. A bigger value will result in a bigger size and intensity.

For `Shininess` and `Specular` examples, see above in the `Directional Light` section.

-   `Diffuse` = `0.2`

![](images/Point_diffuse_0.2.png "images/Point_diffuse_0.2.png")

-   `Diffuse` = `0.5`

![](images/Pointdiffuse0.5.png "images/Pointdiffuse0.5.png")

-   `Diffuse` = `1`

![](images/Pointdiffuse1.png "images/Pointdiffuse1.png")

-   `Diffuse` = `2`

![](images/Pointdiffuse2.png "images/Pointdiffuse2.png")

-   `Attenuation distance` = `5`

![](images/Pointattenuation5.png "images/Pointattenuation5.png")

-   `Attenuation distance` = `10`

![](images/Pointattenuation10.png "images/Pointattenuation10.png")

-   `Attenuation distance` = `18`

![](images/Pointattenuation18.png "images/Pointattenuation18.png")

