In this tutorial, we will see how to use the 3D transforms available in the engine in our custom effects. In the [Create your first custom effect](Create_your_first_custom_effect.md) tutorial, we've seen how to declare uniforms and set them from our application code. But having to manually set each uniform is not really scalable, especially regarding 3D transforms and the camera because this kind of data is likely to change at every frame. Yet, most of our objects will need them in order to be renderer properly.

Step 1: Binding the model to world matrix
-----------------------------------------

In the [Moving objects](Moving_objects.md) tutorial, we've seen that we can add custom 3D transforms to our scene nodes using the Transform component. If you take a look at the code for the Transform::initialize() method, you'll notice that this very component declares the transform.modelToWorldMatrix in it's [data::Provider](data::Provider):


```cpp
 // Transform.cpp void Transform::initialize() {

//someothercode...

_data->set<Matrix4x4::Ptr>("transform.modelToWorldMatrix",_modelToWorld);

} 
```


When the Transform component is added to some target Node, it will add its [data::Provider](data::Provider) to this Node's [data::Container](data::Container). The immediate result is that the transform.modelToWorldMatrix is then available and can be bound in the uniformBindings of our effect:


```javascript
 "uniformBindings" : {

"uModelToWorldMatrix":"transform.modelToWorldMatrix"

} 
```


If we add this to the code from the [Creating custom materials](Creating_custom_materials.md) tutorial, we end up with the following code for our effect:


```javascript
 {

"name":"MyCustomEffect",
"attributeBindings":{
"aPosition":"geometry[${geometryId}].position"
},
"uniformBindings":{
"uColor":"material[${materialId}].color",
"uModelToWorldMatrix":"transform.modelToWorldMatrix"
},
"passes":[{
"vertexShader":"
#ifdefGL_ES
precisionmediumpfloat;
#endif
attributevec3aPosition;
uniformmat4uModelToWorldMatrix;
uniformmat4uViewMatrix;
uniformmat4uProjectionMatrix;
voidmain(void)
{
gl_Position=uProjectionMatrix*uViewMatrix*uModelToWorldMatrix*vec4(aPosition,1.0);
}
",
"fragmentShader":"
#ifdefGL_ES
precisionmediumpfloat;
#endif
uniformvec4uColor;
voidmain(void)
{
gl_FragColor=uColor;
}
"
}]

} 
```


You can learn more about the *.effect files format in the [Effect files format reference](Effect_files_format_reference.md) article. To learn more about data binding, please read the [Understanding data binding](Understanding_data_binding.md) article.

Step 2: Udpating the application code
-------------------------------------

Because our uModelToWorldMatrix property is now bound to transform.modelToWorldMatrix, we have to update our application code to:

-   avoid setting uModelToWorldMatrix directly: it will be set automatically by data binding;
-   make sure our scene Node actually has a Transform component, otherwise the uModelToWorldMatrix will not be bound and rendering might be broken.


```cpp
 auto cube = scene::Node::create()

->addComponent(Transform::create(
Matrix4x4::create()->translation(0.f,0.f,-10.f)
))
->addComponent(Surface::create(
geometry::CubeGeometry::create(),
myCustomMaterial,
myCustomEffect
));


```


Note how we initialize our Transform component with the translation Matrix4x4 we used to use as the value to set uModelToWorldMatrix. But thanks to data binding, this uniform will now be automatically be updated everytime we change the Transform::transform() property.

You can read more about the Transform component in the [Moving objects](Moving_objects.md) tutorial.

Final code
----------

asset/effect/MyCustomEffect.effect 
```javascript
 {

"name":"MyCustomEffect",
"attributeBindings":{
"aPosition":"geometry[${geometryId}].position"
},
"uniformBindings":{
"uColor":"material[${materialId}].color",
"uModelToWorldMatrix":"transform.modelToWorldMatrix"
},
"passes":[{
"vertexShader":"
#ifdefGL_ES
precisionmediumpfloat;
#endif
attributevec3aPosition;
uniformmat4uModelToWorldMatrix;
uniformmat4uViewMatrix;
uniformmat4uProjectionMatrix;
voidmain(void)
{
gl_Position=uProjectionMatrix*uViewMatrix*uModelToWorldMatrix*vec4(aPosition,1.0);
}
",
"fragmentShader":"
#ifdefGL_ES
precisionmediumpfloat;
#endif
uniformvec4uColor;
voidmain(void)
{
gl_FragColor=uColor;
}
"
}]

} 
```


src/main.cpp 
```cpp
 #include "minko/Minko.hpp" #include "minko/MinkoSDL.hpp"

#include "MyCustomMaterial.hpp"

using namespace minko; using namespace minko::math; using namespace minko::component;

const uint WINDOW\WIDTH = 800; const uint WINDOW\HEIGHT = 600;

int main(int argc, char** argv) {

autocanvas=Canvas::create("MinkoTutorial-Bindingthemodeltoworldtransform",WINDOW_WIDTH,WINDOW_HEIGHT);
autosceneManager=component::SceneManager::create(canvas->context());
sceneManager->assets()->queue("effect/MyCustomEffect.effect");
autocomplete=sceneManager->assets()->complete()->connect([&](file::AssetLibrary::Ptrassets)
{
autoroot=scene::Node::create("root")
->addComponent(sceneManager)
->addComponent(Renderer::create(0x7f7f7fff));
automyCustomEffect=assets->effect("effect/MyCustomEffect.effect");
automyCustomMaterial=material::MyCustomMaterial::create();
autocube=scene::Node::create("cube")
->addComponent(Transform::create(
Matrix4x4::create()->translation(0.f,0.f,-10.f)
))
->addComponent(Surface::create(
geometry::CubeGeometry::create(assets->context()),
myCustomMaterial,
myCustomEffect
));
root->addChild(cube);

myCustomMaterial->color(Vector4::create(1.f,0.f,0.f,1.f));
myCustomEffect->setUniform("uViewMatrix",Matrix4x4::create());
myCustomEffect->setUniform("uProjectionMatrix",Matrix4x4::create()->perspective((float)PI*0.25f,(float)WINDOW_WIDTH/(float)WINDOW_HEIGHT,.1f,1000.f));
autoenterFrame=canvas->enterFrame()->connect([&](Canvas::Ptrcanvas,floatt,floatdt)
{
cube->component<Transform>()->transform()->prependRotationY(0.01f);
sceneManager->nextFrame(t,dt);
});
canvas->run();
});
sceneManager->assets()->load();
return0;

} 
```


