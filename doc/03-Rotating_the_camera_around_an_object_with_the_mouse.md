In this tutorial, we will see how to catch mouse inputs in order to rotate our camera.

The code for this tutorial is based on the one described in the [Hello cube!](Hello_cube!.md) tutorial.

Step 1: Catching mouse inputs
-----------------------------

To get the mouse inputs, we will listen to the Canvas::mouseMove() signal:


```cpp
 auto mouseMove = canvas->mouse()->move()->connect([&](input::Mouse::Ptr mouse, int dx, int dy) {

std::cout<<"dx:"<<dx<<",dy:"<<dy<<std::endl;

}); 
```


Moving something everytime the mouse move is not really user friendly. A nicer behavior is to start listeing to the mouse motion when its left button is down and stop when it is released:


```cpp
 Signal<input::Mouse::Ptr, int, int>::Slot mouseMove;

auto mouseDown = canvas->mouse()->leftButtonDown()->connect([&](input::Mouse::Ptr mouse) {

mouseMove=canvas->mouse()->move()->connect([&](input::Mouse::Ptrmouse,intdx,intdy)
{
std::cout<<"dx:"<<dx<<",dy:"<<dy<<std::endl;
});

});

auto mouseUp = canvas->mouse()->leftButtonUp()->connect([&](input::Mouse::Ptr mouse) {

mouseMove=nullptr;

}); 
```


Setting mouseMove to nullptr in the callback for the Canvas::mouseLeftButtonUp() signal will actually remove the associated callback. Thus, as soon as the user releases the mouse left button, the Canvas::mouseMove() signal will stopped being listened to.

Step 2: Rotating the camera
---------------------------

To be able to rotate our camera, we have to make sure it actually has a Transform. To do this, we will update the camera initialization code as follow:


```cpp
 auto camera = scene::Node::create("camera")

->addComponent(Renderer::create(0x7f7f7fff))
->addComponent(Transform::create(
Matrix4x4::create()->lookAt(Vector3::zero(),Vector3::create(0.,0.,-5.f))
))
->addComponent(PerspectiveCamera::create(
(float)WINDOW_WIDTH/(float)WINDOW_HEIGHT,(float)PI*0.25f,.1f,1000.f)
);


```


Now that our camera has a Transform, we can use this very component to alter its rotation:


```cpp
 auto mouseDown = canvas->mouse()->leftButtonDown()->connect([&](input::Mouse::Ptr mouse) {

mouseMove=canvas->mouse()->move()->connect([&](input::Mouse::Ptrmouse,intdx,intdy)
{
camera->component<Transform>()->matrix()->appendRotationY((float)dx*.1f);
});

}); 
```


The dx argument gives the actual position difference of the mouse cursor on the x axis. We can then rotate the camera on the Y axis with an angle delta computed from the difference between the new and the old x position of the mouse cursor.

Step 3: Adding inertia
----------------------

To get a smoother feeling for our camera rotation, we will add a bit of inertia. To do this, we must introduce a cameraRotationSpeed floatting point value:


```cpp
 float camerationRotationSpeed = 0.f;

auto mouseDown = canvas->mouse()->leftButtonDown()->connect([&](input::Mouse::Ptr mouse) {

mouseMove=canvas->mouse()->move()->connect([&](input::Mouse::Ptrmouse,intdx,intdy)
{
cameraRotationSpeed=(float)dx*.01f;
});

}); 
```


We will then use this value at each frame to rotate our camera:


```cpp
 auto enterFrame = canvas->enterFrame()->connect([&](Canvas::Ptr canvas, float t, float dt) {

camera->component<Transform>()->matrix()->appendRotationY(camerationRotationSpeed);
camerationRotationSpeed*=.99f;

sceneManager->nextFrame(t,dt);

}); 
```


Right after rotating the camera, we scale down its rotation speed by a 0.99 factor to get a smaller rotation next frame and so on... to produce a nice exponential interpolation.

Final code
----------


```cpp
 #include "minko/Minko.hpp" #include "minko/MinkoSDL.hpp"

using namespace minko; using namespace minko::math; using namespace minko::component;

const uint WINDOW\WIDTH = 800; const uint WINDOW\HEIGHT = 600;

int main(int argc, char** argv) {

autocanvas=Canvas::create("Tutorial-Rotatingthecameraaroundanobjectwiththemouse",WINDOW_WIDTH,WINDOW_HEIGHT);
autosceneManager=component::SceneManager::create(canvas->context());

//WereplacethebasiceffectbythePhongeffecttohavelighteffects
sceneManager->assets()->queue("effect/Phong.effect");
autocomplete=sceneManager->assets()->complete()->connect([&](file::AssetLibrary::Ptrassets)
{
autoroot=scene::Node::create("root")
->addComponent(sceneManager);

autocamera=scene::Node::create("camera")
->addComponent(Renderer::create(0x7f7f7fff))
->addComponent(Transform::create(
Matrix4x4::create()->lookAt(Vector3::zero(),Vector3::create(0.,0.,-5.f))
))
->addComponent(PerspectiveCamera::create(
(float)WINDOW_WIDTH/(float)WINDOW_HEIGHT,(float)PI*0.25f,.1f,1000.f)
);
root->addChild(camera);

//Addasimpledirectionallighttoreallyseethecamerarotation
autodirectionalLight=scene::Node::create("directionalLight")
->addComponent(DirectionalLight::create())
->addComponent(Transform::create(Matrix4x4::create()->lookAt(
Vector3::create(-0.33f,-0.33f,0.33f),Vector3::create())));
root->addChild(directionalLight);

//Replacethecubebyaspheretoinscreaselightvisibility
autosphere=scene::Node::create("sphere")
->addComponent(Surface::create(
geometry::SphereGeometry::create(assets->context()),
material::BasicMaterial::create()->diffuseColor(Vector4::create(0.f,0.f,1.f,1.f)),
assets->effect("effect/Phong.effect")
));
root->addChild(sphere);

Signal<input::Mouse::Ptr,int,int>::SlotmouseMove;
floatcameraRotationSpeed=0.f;

automouseDown=canvas->mouse()->leftButtonDown()->connect([&](input::Mouse::Ptrmouse)
{
mouseMove=canvas->mouse()->move()->connect([&](input::Mouse::Ptrmouse,intdx,intdy)
{
cameraRotationSpeed=(float)-dx*.01f;
});
});

automouseUp=canvas->mouse()->leftButtonUp()->connect([&](input::Mouse::Ptrmouse)
{
mouseMove=nullptr;
});

autoenterFrame=canvas->enterFrame()->connect([&](Canvas::Ptrcanvas,floatt,floatdt)
{
camera->component<Transform>()->matrix()->appendRotationY(cameraRotationSpeed);
cameraRotationSpeed*=.99f;

sceneManager->nextFrame(t,dt);
});

canvas->run();
});

sceneManager->assets()->load();

return0;

} 
```


