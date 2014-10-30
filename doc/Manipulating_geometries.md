The `Geometry` section of the `Properties` panel provides a set of operations you can perform on geometries.

Flip normals
============

This will invert all normals of your geometry. Normals will impact the light effects on a surface.

-   Default normals

![Default normals](images/Flip_normals1.png "Default normals")

-   Flipped normals

![Flipped normals](images/Flip_normals2.png "Flipped normals")

Flip Tangents
=============

This will invert the tangents of your geometry. Tangents are used with the normal maps of your materials.

-   Default tangents

![](images/Flip_tangents1.png "images/Flip_tangents1.png")

-   Flipped tangents

![](images/Flip_tangents2.png "images/Flip_tangents2.png")

Invert winding
==============

This will invert the winding of each triangle of the geometry.

-   Default winding

![](images/Windings1.png "images/Windings1.png")

-   Inverted winding

![](images/Windings2.png "images/Windings2.png")

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

![](images/Applytransform1.png "images/Applytransform1.png")

-   Cube geometry with the mesh tranform applied to it

![](images/Applytransform2.png "images/Applytransform2.png")

Center Geometry
===============

This will set the geometry origin to the center of its bounding box. If a mesh uses this geometry, its transform will be changed so that the geometry keeps its place in space.

-   Offseted geometry

![](images/Centergeometry1.png "images/Centergeometry1.png")

-   Centered geometry

![](images/Centergeometry2.png "images/Centergeometry2.png")

