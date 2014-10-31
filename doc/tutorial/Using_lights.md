You can add 4 different type of lights in your scene for this, open the right click menu on the scene tree where you want to add your light, and go in the `Add Light` submenu.

Ambient Light
=============

An ambient light will affect all objects in the scene and light them equally on all surface.

-   `Color`: changes the light color
-   `Ambient`: changes the intensity of the light. All materials can accentuate this intensity with the `Ambient Multiply` parameter.
-   `Emission`: sets the emission mask for the light. Any material with a layer enabled in its `reception` mask will be affected by the light if this same layer is enabled in the `emission` mask

 

-   Ambient = 0

![](../image/Ambient0.png "../image/Ambient0.png")

-   Ambient = 0.5

![](../image/Ambient0.5.png "../image/Ambient0.5.png")

-   Ambient = 1

![](../image/Ambient1.png "../image/Ambient1.png")

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

![](../image/Dirdiffuse0.1.png "../image/Dirdiffuse0.1.png")

-   Diffuse = 0.3

![](../image/Dirdiffuse0.3.png "../image/Dirdiffuse0.3.png")

-   Diffuse = 0.6

![](../image/Dirdiffuse0.6.png "../image/Dirdiffuse0.6.png")

-   Shininess = 1024

![](../image/Dirshininess1024.png "../image/Dirshininess1024.png")

-   Shininess = 128

![](../image/Dirshininess128.png "../image/Dirshininess128.png")

-   Shininess = 40

![](../image/Dirshininess40.png "../image/Dirshininess40.png")

-   Specular = 0

![](../image/Dirspecular0.png "../image/Dirspecular0.png")

-   Specular = 0.3

![](../image/Dirspecular0.3.png "../image/Dirspecular0.3.png")

-   Specular = 0.8

![](../image/Dirspecular0.8.png "../image/Dirspecular0.8.png")

-   Specular = 2

![](../image/Dirspecular2.png "../image/Dirspecular2.png")

Shadows
-------

### Common Parameters

-   `Map Size`: size of the map used to draw shadows to. A bigger size will result in better, cleaner shadows, but a smaller size will be better for performance.
-   `Quality`: changes the way shadows are computed. Higher quality could impact on the performances.
-   `Map width`: width on which the shadows will be computed. Will be represented on screen by the light frustum. The position of this frustum will depend on the light `position`.
-   `Z-far`: maximum distance on which the shadows will be produced. Will be represented on screen by the light frustum.

 

-   Small `map width`: the shadows of the cube and torus are cut.

![](../image/Dirshadowsmallfrustum.png "../image/Dirshadowsmallfrustum.png")

-   Larger `map width`: the shadows of the cube and torus are fully visible.

![](../image/Dirshadowlargerfrustum.png "../image/Dirshadowlargerfrustum.png")

-   `Map size` = `64` `Quality` = Hard

![](../image/Dirshadowhard64.png "../image/Dirshadowhard64.png")

-   `Map size` = `512` `Quality` = Medium

![](../image/Dirshadowmedium512.png "../image/Dirshadowmedium512.png")

### Shadow mapping types

Minko provides two different shadow types.

-   `ESM`: exponential shadow mapping.
-   `PCF `: percentage-closer shadow mapping.

#### ESM

The ESM filters the shadow map by approximating the shadow test with an exponential function.

-   `Exponential factor`: a bigger value will give a better approximation

`ESM` works better with smaller `Z-far` and `Map width`.

-   `Exponential factor` = `1.5`, the two cube shadows have a slightly different color

![](../image/Esmexp1.5.png "../image/Esmexp1.5.png")

-   `Exponential factor` = `10`, the two cube shadows have the same color and blend in an uniform shadow

![](../image/Esmexp10.png "../image/Esmexp10.png")

#### PCF

`PCF` will filter the shadow map by calculating how far from the light the shadow is, producing sharper edges closer to the light and smoother ones further from the light.

-   `Bias`
-   `Spread`: how much the shadow will spread when it is far from the light

 

-   `Spread` = `0`, the shadow edges are sharp.

![](../image/Pcfspread.png "../image/Pcfspread.png")

-   `Spread` = `0`, the shadow edges are smoothed.

![](../image/Pcfspread15.png "../image/Pcfspread15.png")

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

![](../image/Spotdif0.5.png "../image/Spotdif0.5.png")

-   `Diffuse` = `1`

![](../image/Spotdif1.png "../image/Spotdif1.png")

-   `Diffuse` = `5`

![](../image/Spotdif5.png "../image/Spotdif5.png")

-   Small `outer radius` and `inner radius`

![](../image/Spotsmallradius.png "../image/Spotsmallradius.png")

-   Bigger `outer radius`

![](../image/Spotmediumradius.png "../image/Spotmediumradius.png")

-   Bigger `outer radius` and `inner radius` close to the `outer radius`

![](../image/Spotbigradius.png "../image/Spotbigradius.png")

-   Small `Attenuation distance`

![](../image/Spotsmallattenuation.png "../image/Spotsmallattenuation.png")

-   Medium `Attenuation distance`

![](../image/Spotmediumattenuation.png "../image/Spotmediumattenuation.png")

-   Larger `Attenuation distance`

![](../image/Spotbigattenuation.png "../image/Spotbigattenuation.png")

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

![](../image/Point_diffuse_0.2.png "../image/Point_diffuse_0.2.png")

-   `Diffuse` = `0.5`

![](../image/Pointdiffuse0.5.png "../image/Pointdiffuse0.5.png")

-   `Diffuse` = `1`

![](../image/Pointdiffuse1.png "../image/Pointdiffuse1.png")

-   `Diffuse` = `2`

![](../image/Pointdiffuse2.png "../image/Pointdiffuse2.png")

-   `Attenuation distance` = `5`

![](../image/Pointattenuation5.png "../image/Pointattenuation5.png")

-   `Attenuation distance` = `10`

![](../image/Pointattenuation10.png "../image/Pointattenuation10.png")

-   `Attenuation distance` = `18`

![](../image/Pointattenuation18.png "../image/Pointattenuation18.png")

