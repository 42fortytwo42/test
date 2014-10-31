The `Geometry` section of the `Properties` panel provides a set of operations you can perform on geometries.

Flip normals
============

This will invert all normals of your geometry. Normals will impact the light effects on a surface.

-   Default normals

![Default normals](../image/Flip_normals1.png "Default normals")

-   Flipped normals

![Flipped normals](../image/Flip_normals2.png "Flipped normals")

Flip Tangents
=============

This will invert the tangents of your geometry. Tangents are used with the normal maps of your materials.

-   Default tangents

![](../image/Flip_tangents1.png "../image/Flip_tangents1.png")

-   Flipped tangents

![](../image/Flip_tangents2.png "../image/Flip_tangents2.png")

Invert winding
==============

This will invert the winding of each triangle of the geometry.

-   Default winding

![](../image/Windings1.png "../image/Windings1.png")

-   Inverted winding

![](../image/Windings2.png "../image/Windings2.png")

Compute Normals
===============

This will automatically compute the normals of the geometry.

Compute Tangents
================

This will automatically compute the tangents of the geometry.

Apply Transform
===============

If you select a mesh node, you can apply its transform to the geometry it uses. It will duplicate the geometry and apply the mesh transform to it. The selected mesh will then use this new geometry and its transform will be set to identity.

-   Default cube geometry

![](../image/Applytransform1.png "../image/Applytransform1.png")

-   Cube geometry with the mesh tranform applied to it

![](../image/Applytransform2.png "../image/Applytransform2.png")

Center Geometry
===============

This will set the geometry origin to the center of its bounding box. If a mesh uses this geometry, its transform will be changed so that the geometry keeps its place in space.

-   Offseted geometry

![](../image/Centergeometry1.png "../image/Centergeometry1.png")

-   Centered geometry

![](../image/Centergeometry2.png "../image/Centergeometry2.png")

