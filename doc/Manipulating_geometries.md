The `Geometry` section of the `Properties` panel provides a set of operations you can perform on geometries.

Flip normals
============

This will invert all normals of your geometry. Normals will impact the light effects on a surface.

-   Default normals

![Default normals](flip normals1.png "Default normals")

-   Flipped normals

![Flipped normals](flip normals2.png "Flipped normals")

Flip Tangents
=============

This will invert the tangents of your geometry. Tangents are used with the normal maps of your materials.

-   Default tangents

![](flip tangents1.png "flip tangents1.png")

-   Flipped tangents

![](flip tangents2.png "flip tangents2.png")

Invert winding
==============

This will invert the winding of each triangle of the geometry.

-   Default winding

![](windings1.png "windings1.png")

-   Inverted winding

![](windings2.png "windings2.png")

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

![](applytransform1.png "applytransform1.png")

-   Cube geometry with the mesh tranform applied to it

![](applytransform2.png "applytransform2.png")

Center Geometry
===============

This will set the geometry origin to the center of its bounding box. If a mesh uses this geometry, its transform will be changed so that the geometry keeps its place in space.

-   Offseted geometry

![](centergeometry1.png "centergeometry1.png")

-   Centered geometry

![](centergeometry2.png "centergeometry2.png")

