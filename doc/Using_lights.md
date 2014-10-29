You can add 4 different type of lights in your scene for this, open the right click menu on the scene tree where you want to add your light, and go in the `Add Light` submenu.

Ambient Light
=============

An ambient light will affect all objects in the scene and light them equally on all surface.

-   `Color`: changes the light color
-   `Ambient`: changes the intensity of the light. All materials can accentuate this intensity with the `Ambient Multiply` parameter.
-   `Emission`: sets the emission mask for the light. Any material with a layer enabled in its `reception` mask will be affected by the light if this same layer is enabled in the `emission` mask

<!-- -->

-   Ambient = 0

![](ambient0.png "ambient0.png")

-   Ambient = 0.5

![](ambient0.5.png "ambient0.5.png")

-   Ambient = 1

![](ambient1.png "ambient1.png")

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

<!-- -->

-   Diffuse = 0.1

![](dirdiffuse0.1.png "dirdiffuse0.1.png")

-   Diffuse = 0.3

![](dirdiffuse0.3.png "dirdiffuse0.3.png")

-   Diffuse = 0.6

![](dirdiffuse0.6.png "dirdiffuse0.6.png")

-   Shininess = 1024

![](dirshininess1024.png "dirshininess1024.png")

-   Shininess = 128

![](dirshininess128.png "dirshininess128.png")

-   Shininess = 40

![](dirshininess40.png "dirshininess40.png")

-   Specular = 0

![](dirspecular0.png "dirspecular0.png")

-   Specular = 0.3

![](dirspecular0.3.png "dirspecular0.3.png")

-   Specular = 0.8

![](dirspecular0.8.png "dirspecular0.8.png")

-   Specular = 2

![](dirspecular2.png "dirspecular2.png")

Shadows
-------

### Common Parameters

-   `Map Size`: size of the map used to draw shadows to. A bigger size will result in better, cleaner shadows, but a smaller size will be better for performance.
-   `Quality`: changes the way shadows are computed. Higher quality could impact on the performances.
-   `Map width`: width on which the shadows will be computed. Will be represented on screen by the light frustum. The position of this frustum will depend on the light `position`.
-   `Z-far`: maximum distance on which the shadows will be produced. Will be represented on screen by the light frustum.

<!-- -->

-   Small `map width`: the shadows of the cube and torus are cut.

![](dirshadowsmallfrustum.png "dirshadowsmallfrustum.png")

-   Larger `map width`: the shadows of the cube and torus are fully visible.

![](dirshadowlargerfrustum.png "dirshadowlargerfrustum.png")

-   `Map size` = `64` `Quality` = Hard

![](dirshadowhard64.png "dirshadowhard64.png")

-   `Map size` = `512` `Quality` = Medium

![](dirshadowmedium512.png "dirshadowmedium512.png")

### Shadow mapping types

Minko provides two different shadow types.

-   `ESM`: exponential shadow mapping.
-   `PCF `: percentage-closer shadow mapping.

#### ESM

The ESM filters the shadow map by approximating the shadow test with an exponential function.

-   `Exponential factor`: a bigger value will give a better approximation

`ESM` works better with smaller `Z-far` and `Map width`.

-   `Exponential factor` = `1.5`, the two cube shadows have a slightly different color

![](esmexp1.5.png "esmexp1.5.png")

-   `Exponential factor` = `10`, the two cube shadows have the same color and blend in an uniform shadow

![](esmexp10.png "esmexp10.png")

#### PCF

`PCF` will filter the shadow map by calculating how far from the light the shadow is, producing sharper edges closer to the light and smoother ones further from the light.

-   `Bias`
-   `Spread`: how much the shadow will spread when it is far from the light

<!-- -->

-   `Spread` = `0`, the shadow edges are sharp.

![](pcfspread.png "pcfspread.png")

-   `Spread` = `0`, the shadow edges are smoothed.

![](pcfspread15.png "pcfspread15.png")

Spot Light
==========

The light from a `spot light` originates from a point and is diffused in a cone.

Transform properties
--------------------

-   `Position`: position from which the `spot light` will emit.
-   `Target Position`: point to which the cone of the `spot light` will point.

Light properties
----------------

-   `Color\</color\>: changes the light color.
-   `Attenuation Distance`: distance at which the light intensity will fade out.
-   `Inner radius`, `Outer radius`: the `outer radius` gives the radius of the cone, the light will be more intense inside of the `inner radius` and will fade from the `inner radius` to the `outer radius`.
-   `Diffuse`: changes the intensity of the light. All materials can accentuate this intensity with the `Diffuse Multiplier` parameter.
-   `Shininess`: this will affect the spread of the specular spot. A bigger value will result in a smaller spot.
-   `Specular`: this will affect the intensity and radius of the light specular spot. A bigger value will result in a bigger size and intensity.

For `Shininess` and `Specular` examples, see above in the `Directional Light` section.

-   `Diffuse` = `0.5`

![](spotdif0.5.png "spotdif0.5.png")

-   `Diffuse` = `1`

![](spotdif1.png "spotdif1.png")

-   `Diffuse` = `5`

![](spotdif5.png "spotdif5.png")

-   Small `outer radius` and `inner radius`

![](spotsmallradius.png "spotsmallradius.png")

-   Bigger `outer radius`

![](spotmediumradius.png "spotmediumradius.png")

-   Bigger `outer radius` and `inner radius` close to the `outer radius`

![](spotbigradius.png "spotbigradius.png")

-   Small `Attenuation distance`

![](spotsmallattenuation.png "spotsmallattenuation.png")

-   Medium `Attenuation distance`

![](spotmediumattenuation.png "spotmediumattenuation.png")

-   Larger `Attenuation distance`

![](spotbigattenuation.png "spotbigattenuation.png")

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

![](point diffuse 0.2.png "point diffuse 0.2.png")

-   `Diffuse` = `0.5`

![](pointdiffuse0.5.png "pointdiffuse0.5.png")

-   `Diffuse` = `1`

![](pointdiffuse1.png "pointdiffuse1.png")

-   `Diffuse` = `2`

![](pointdiffuse2.png "pointdiffuse2.png")

-   `Attenuation distance` = `5`

![](pointattenuation5.png "pointattenuation5.png")

-   `Attenuation distance` = `10`

![](pointattenuation10.png "pointattenuation10.png")

-   `Attenuation distance` = `18`

![](pointattenuation18.png "pointattenuation18.png")

