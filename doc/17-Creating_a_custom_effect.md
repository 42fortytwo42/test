In this tutorial you wil learn how to create your very own custom rendering effect. We will see three main things:

-   the anatomy of a simple `\*.effect` file;
-   how to write a simple GLSL shader;
-   how to load and use such effect in your application.

Understanding how effects work is very important because they control the final color of each pixel on the screen. The effects you use and how you use them will determine the very look of your application. Here, we will just create a very simple effect that renders a solid color. But with the following tutorials, reading Minko's core framework `\*.effect` files and learning GLSL should help you creating increasingly amazing effects.

Step 1: Creating the effect file
--------------------------------

In Minko, rendering effects are stored in separate `\*.effect` files. Indeed, Minko has what is called a "data driven" rendering pipeline: it means the rendering system is entirely configurable through external data or "declarative" files. Those files are `\*.effect` files.

`\*.effect` files store all the required data to configure the rendering pipeline. As such, they are the perfect way to create complex, rich and beautiful rendering programs that can easily be reused, shared and distributed.

Here is a simple `\*.effect` file skeleton that will help us getting started:


```
 {

` "name" : "MyCustomEffect",`
` "attributeBindings" : {`
`   "aPosition" : "geometry[${geometryId}].position"`
` },`
` "passes" : [{`
`   "vertexShader" : "`
`     // my custom vertex shader GLSL code...`
`   ",`
`   "fragmentShader" : "`
`     // my custom fragment shader GLSL code...`
`   "`
` }]`

} 
```


Save this in a `MyCustomEffect.effect` file in the `asset/effect` folder of your app.

As you can see, `\*.effect` files are declared using the JSON format. Here are a few details about the code sample above:

-   the `name` field declares the name of our effect; when loaded our effect will be referenced in the `AssetLibrary` by 1) the actual file name used for loading 2) the value of this "name" field
-   the `attributeBindings` field declares an object that will map our effect's shaders (vertex) attribute declarations to actual engine data properties
-   the `passes` field declares an array of objects where each object is a rendering pass made mainly of a [vertex shader](https://en.wikipedia.org/wiki/Shader#Vertex_shaders) (the "vertexShader" field) and a [fragment shader](https://en.wikipedia.org/wiki/Shader#Pixel_shaders) (the "fragmentShader" field).

You can learn more about the `\*.effect` files format in the [Effect files format reference](Effect_files_format_reference.md) article.

Step 2 : The vertex shader
--------------------------

We can now define our vertex shader for the single and only pass of our effect. Our vertex shader will simply:

1.  take the local 3D model-space position of vertex by declaring the `aPosition` atribute,
2.  transform it to be in the global world-space by multiplying `aPosition` by `uModelToWorldMatrix`,
3.  transform it again to be in the camera-relative view-space by multiplying the previous result by `uViewMatrix`,
4.  project it on the 2D screen by multiplying the previous result by `uProjectionMatrix`.


```


1.  ifdef GL\ES

precision mediump float;

1.  endif

attribute vec3 aPosition;

uniform mat4 uModelToWorldMatrix; uniform mat4 uViewMatrix; uniform mat4 uProjectionMatrix;

void main(void) {

` gl_Position = uProjectionMatrix * uViewMatrix * uModelToWorldMatrix * vec4(aPosition, 1.0);`

} 
```


Note how we declare a default `mediump` precision specifier if the `GL\ES` macro is defined: it is mandatory if we want to target OpenGL ES 2.0 (WebGL and mobile devices).

Here, we've declared a (vertex) `attribute` and 3 `uniform`s. The `attribute` should be filled properly thanks to the `attributeBindings` declared in our `\*.effect` file. We don't know yet how it works exactly but it should work. Yet, our `uniform`s don't have a value and no bindings declared: we will have to set them at runtime when our effect is loaded.

Step 3: The fragment shader
---------------------------

Our fragment shader will be even simpler:

-   we declare a single `uniform` that will hold an RGBA color;
-   we set this color to be the final color of our pixel by assigning it to `gl\FragColor`.


```


1.  ifdef GL\ES

precision mediump float;

1.  endif

uniform vec4 uColor;

void main(void) {

` gl_FragColor = uColor;`

} 
```


Step 4: Loading and using our custom effect
-------------------------------------------

We can now load our `MyCustomEffect.effect` effect in our application and use it for rendering! To do this, we just have to:

-   load the `\*.effect` file in the `AssetLibrary`
-   fetch back the corresponding `Effect` object created upon loading
-   use this very `Effect` object to initialize our `Surface`


```
 sceneManager->assets()->queue("effect/MyCustomEffect.effect");

sceneManager->assets()->complete()->connect([&](file::AssetLibrary:Ptr assets) {

` auto myCustomEffect = assets->effect("effect/MyCustomEffect.effect");`

` auto cube = scene::Node::create()->addComponent(Surface::create(`
`   geometry::CubeGeometry::create(assets->context()),`
`   material::Material::create(),`
`   myCustomEffect`
` ));`

}); 
```


But for our custom `Effect` to work, we need to fill properly all the `uniform` values it expects. To do this, we will use the `Effect::setUniform()` method:


```
 myCustomEffect->setUniform("uModelToWorldMatrix", Matrix4x4::create()->translation(0.f, 0.f, -5.f)); myCustomEffect->setUniform("uViewMatrix", Matrix4x4::create()); myCustomEffect->setUniform("uProjectionMatrix", Matrix4x4::create()->perspective((float)PI \* 0.25f, (float)WINDOW\WIDTH / (float)WINDOW\HEIGHT, .1f, 1000.f)); myCustomEffect->setUniform("uColor", Vector4::create(0.f, 0.f, 1.f, 1.f)); 
```


Final code
----------

asset/effect/MyCustomEffect.effect 
```
 {

` "name" : "MyCustomEffect",`
` "attributeBindings" : {`
`   "aPosition" : "geometry[${geometryId}].position"`
` },`
` "passes" : [{`
`   "vertexShader" : "`
`     #ifdef GL_ES`
`     precision mediump float;`
`     #endif`

`     attribute vec3 aPosition;`

`     uniform mat4 uModelToWorldMatrix;`
`     uniform mat4 uViewMatrix;`
`     uniform mat4 uProjectionMatrix;`

`     void main(void)`
`     {`
`       gl_Position = uProjectionMatrix * uViewMatrix * uModelToWorldMatrix * vec4(aPosition, 1.0);`
`     }`
`   ",`
`   "fragmentShader" : "`
`     #ifdef GL_ES`
`     precision mediump float;`
`     #endif`

`     uniform vec4 uColor;`

`     void main(void)`
`     {`
`       gl_FragColor = uColor;`
`     }`
`   "`
` }]`

} 
```


src/main.cpp 
```


1.  include "minko/Minko.hpp"
2.  include "minko/MinkoSDL.hpp"

using namespace minko; using namespace minko::math; using namespace minko::component;

const uint WINDOW\WIDTH = 800; const uint WINDOW\HEIGHT = 600;

int main(int argc, char\*\* argv) {

` auto canvas = Canvas::create("Minko Tutorial - Create your first custom effect", WINDOW_WIDTH, WINDOW_HEIGHT);`
` auto sceneManager = component::SceneManager::create(canvas->context());`
` sceneManager->assets()->queue("effect/Basic.effect");`
` auto complete = sceneManager->assets()->complete()->connect([&](file::AssetLibrary::Ptr assets)`
` {`
`   auto myCustomEffect = assets->effect("effect/MyCustomEffect.effect");`

`   auto root = scene::Node::create("root")`
`     ->addComponent(sceneManager)`
`     ->addComponent(Renderer::create(0x7f7f7fff));`
`   auto cube = scene::Node::create("cube")`
`     ->addComponent(Surface::create(`
`       geometry::CubeGeometry::create(assets->context()),`
`       material::BasicMaterial::create()->diffuseColor(Vector4::create(0.f, 0.f, 1.f, 1.f)),`
`       myCustomEffect`
`     ));`
`   root->addChild(cube);`

`   autoModelToWorldMatrix = Matrix4x4::create()->translation(0.f, 0.f, -5.f);`

`   myCustomEffect->setUniform("uModelToWorldMatrix", modelToWorldMatrix);`
`   myCustomEffect->setUniform("uViewMatrix", Matrix4x4::create());`
`   myCustomEffect->setUniform("uProjectionMatrix", Matrix4x4::create()->perspective((float)PI * 0.25f, (float)WINDOW_WIDTH / (float)WINDOW_HEIGHT, .1f, 1000.f));`
`   myCustomEffect->setUniform("uColor", Vector4::create(0.f, 0.f, 1.f, 1.f));`
`   auto enterFrame = canvas->enterFrame()->connect([&](Canvas::Ptr canvas, float t, float dt)`
`   {`
`     modelToWorldMatrix->prependRotationY(0.01f);`
`     myCustomEffect->setUniform("uModelToWorldMatrix", modelToWorldMatrix);`
`     `
`     sceneManager->nextFrame(t, dt);`
`   });`
`   canvas->run();`
` });`
` sceneManager->assets()->load();`
` return 0;`

} 
```


Where to go from there
----------------------

As you might have noticed, our `Effect` is not really easy to work with:

-   setting uniforms will affect all the objects rendered with that `Effect`; to solve this you can read the [Creating custom materials](Creating_custom_materials.md) tutorial;
-   we have to deal with our model to world transform manually; to solve this you can read the [Binding the model to world transform](Binding_the_model_to_world_transform.md) tutorial;
-   we are setting/updating the camera manually with a view and a project matrix; to solve this you can read the [Binding the camera](Binding_the_camera.md) tutorial
