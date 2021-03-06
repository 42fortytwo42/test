Transform gizmos
================

With the three left buttons, you can switch between the transform gizmos. These gizmos give you a way to move elements from the scene in a more visual way. The modes are, from left to right :

-   Translation

![](../../doc/image/Gizmo1.png "../../doc/image/Gizmo1.png")

-   Rotation

![](../../doc/image/Gizmo2.png "../../doc/image/Gizmo2.png")

-   Scale

![](../../doc/image/Gizmo3.png "../../doc/image/Gizmo3.png")

Next is the spacial reference for the gizmos. You can move them in `local` space or `world` space ![](../../doc/image/Gizmo4.png "fig:../../doc/image/Gizmo4.png")

Finally, you can choose the point used as pivot point for the rotations. `center` uses the center of the geometric center of the mesh/group, and `pivot` uses either the origin of the mesh/group, or the pivot point if you provided one. ![](../../doc/image/Gizmo5.png "fig:../../doc/image/Gizmo5.png")

For more details on transform manipulation, see the [Manipulating transforms](../tutorial/Manipulating_transforms.md) tutorial.

Animations and physics control
==============================

The next buttons are used to control the animations and the physics world.

Play/Pause button
-----------------

The play button will start the animations, and will start the physics world. When playing, it is replaced by a pause button that will pause the animations and physics simulation.

Stop Button
-----------

This button will stop the animations and reset them to their first frame. It will also stop the physics simulation and reset any physics element to its initial place.

Step button
-----------

This button will step one frame into the animations. It has no effect on the physics world.

Rendering mode
==============

The drop-down list in the middle of the bar allows you to choose between different render modes.

Basic
-----

This mode will render everything with a basic effect, not taking any light into account. ![](../../doc/image/Render_basic.png "fig:../../doc/image/Render_basic.png")

Realistic
---------

This mode will render everything with a phong effect. All lights phong related properties will be taken into account. Note that without any light on your scene, everything will be rendered black.

![](../../doc/image/Renderrealistic.png "../../doc/image/Renderrealistic.png")

Greybox
-------

This mode will render everything in different levels of grey.

![](../../doc/image/Rendergreybox.png "../../doc/image/Rendergreybox.png")

UVs
---

This mode will show how UVs are mapped on each mesh. This is useful for debugging texture mapping problems. ![](../../doc/image/Render_uv.png "fig:../../doc/image/Render_uv.png")

Normals
-------

This mode will show the normals on each mesh.

![](../../doc/image/Render_normals.png "../../doc/image/Render_normals.png")

Visual elements checklist
=========================

This checklist allows you to enable and to disable visual elements on the scene :

-   Grid (the grid on the XZ plan)
-   Light gizmos
-   Highlight (highlighting effect on a selected node)
-   Colliders (visual representation of physics colliders, displayed in wireframe)
-   Selection box (around the bounding box of a selected node)
-   Frustums (a visual representation of the camera and light frustums)
-   Skeleton (a visualisation of animation skeletons)
-   Joints (visual representation of physics joints)

![](../../doc/image/Visual_elements.png "../../doc/image/Visual_elements.png")

Camera type
===========

This button allows you to switch between the `Arc Ball` camera (rotating around the selected node) and the `First Person` camera (moving freely in the scene).

For more details on moving the camera in the scene, see the [Moving the camera in the scene](../tutorial/Moving_the_camera_in_the_scene.md) tutorial.

Multi-selection
===============

The last button allows you to enable and disable multi-selection. When enabled, you can select multiple nodes on the scene by just clicking and dragging your mouse over the nodes you want to select.

![](../../doc/image/Selection.png "../../doc/image/Selection.png")

