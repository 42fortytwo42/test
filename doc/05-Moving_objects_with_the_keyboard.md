In this tutorial, we will see how to catch keyboard inputs and use them to move objects.

Step 1: Catching keyboards inputs
---------------------------------


```cpp
 auto keyDown = canvas->keyboard()->keyDown()->connect([&](input::Keyboard::Ptr k) {

std::cout<<"keydown!"<<std::endl;

}); 
```


The argument passed to the callbacks of the Canvas::keyDown() signal is an array where each cell indicates whether a specific key is down or not.


```cpp
 auto keyDown = canvas->keyboard()->keyDown()->connect([&](input::Keyboard::Ptr k) {

std::cout<<"The'up'keyis"<<(k->keyIsDown(input::Keyboard::ScanCode::SPACE)?"":"not")<<"down"<<std::endl;

}); 
```


Step 2: Moving objects
----------------------

To move our object, we will simply use the Matrix4x4::appendTranslation() method with argument values depending on which key is actually down:


```cpp
 auto keyDown = canvas->keyboard()->keyDown()->connect([&](input::Keyboard::Ptr k) {

if(k->keyIsDown(input::Keyboard::ScanCode::LEFT))
cube->component<Transform>()->matrix()->appendTranslation(-0.1f);
if(k->keyIsDown(input::Keyboard::ScanCode::RIGHT))
cube->component<Transform>()->matrix()->appendTranslation(0.1f);

}); 
```


Final code
----------


```cpp
 #include "minko/Minko.hpp" #include "minko/MinkoSDL.hpp"

using namespace minko; using namespace minko::math; using namespace minko::component;

const uint WINDOW\WIDTH = 800; const uint WINDOW\HEIGHT = 600;

int main(int argc, char** argv) {

autocanvas=Canvas::create("Tutorial-Movingobjectswiththekeyboard",WINDOW_WIDTH,WINDOW_HEIGHT);
autosceneManager=component::SceneManager::create(canvas->context());

sceneManager->assets()->queue("effect/Basic.effect");
autocomplete=sceneManager->assets()->complete()->connect([&](file::AssetLibrary::Ptrassets)
{
autoroot=scene::Node::create("root")
->addComponent(sceneManager);

autocamera=scene::Node::create("camera")
->addComponent(Renderer::create(0x7f7f7fff))
->addComponent(PerspectiveCamera::create(
(float)WINDOW_WIDTH/(float)WINDOW_HEIGHT,(float)PI*0.25f,.1f,1000.f)
);
root->addChild(camera);

autocube=scene::Node::create("cube")
->addComponent(Transform::create(Matrix4x4::create()->translation(0.f,0.f,-5.f)))
->addComponent(Surface::create(
geometry::CubeGeometry::create(assets->context()),
material::BasicMaterial::create()->diffuseColor(Vector4::create(0.f,0.f,1.f,1.f)),
assets->effect("effect/Basic.effect")
));
root->addChild(cube);

autokeyDown=canvas->keyboard()->keyDown()->connect([&](input::Keyboard::Ptrk)
{
if(k->keyIsDown(input::Keyboard::ScanCode::LEFT))
cube->component<Transform>()->matrix()->appendTranslation(-0.1f);
if(k->keyIsDown(input::Keyboard::ScanCode::RIGHT))
cube->component<Transform>()->matrix()->appendTranslation(0.1f);
});

autoenterFrame=canvas->enterFrame()->connect([&](Canvas::Ptrcanvas,floatt,floatdt)
{
sceneManager->nextFrame(t,dt);
});

canvas->run();
});

sceneManager->assets()->load();

return0;

} 
```


