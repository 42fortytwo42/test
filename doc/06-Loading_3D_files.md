This tutorial explains how to use the file loading API. This API is designed to ease the loading of external files of any format. The goal is to give developers the possibility to **load files using the same API regardless of their actual format**.

A file can be loaded from a file or from a url.

Enable ASSIMP
-------------

Assimp is the asset import library used by Minko to load asset files, we have to enable it into the `premake5.lua` with these lines:

```
 minko.plugin.enable("assimp") -- this plugin can be useful for assets that need to load jpeg files minko.plugin.enable("jpeg") ```


The next step is to include the correct header into your C++ application source code.

```


1.  include "minko/MinkoASSIMP.hpp"
2.  include "minko/MinkoJPEG.hpp"

```


Setup file parsers
------------------

Every supported file format is available through a plugin. Each parser must be registered with its associated file format.

In order to enable a data parser, you have to tell Minko it exists using the `AssetLibrary::registerParse` method.

```
 sceneManager-\>assets()

`   ->registerParser<`[`file::ASSIMPParser>`](file::ASSIMPParser>)`("obj")`
`   ->registerParser<`[`file::ASSIMPParser>`](file::ASSIMPParser>)`("dae")`
`       ->registerParser<`[`file::JPEGParser>`](file::JPEGParser>)`("jpg")`

```


Most common 3D file formats are supported by the ASSIMPParser ([Supported file formats](Supported file formats (Community Edition))). To load file with specific Minko extension (lighter, faster and modular), you can read the corresponding tutorial: [Loading .scene files](Loading .scene files). Learn how to export this format from the editor : [Exporting .scene files](Exporting .scene files).

After that, you can add your files to the loading queue and the right parser will be chosen automatically.

Access loaded files
-------------------

Once the loaded complete signal of the assetLibrary is triggered you can access the different model with the `AssetLibrary::symbol(name)` method

```
 auto objModel = assets-\>symbol("model/model.obj"); auto daeModel = assets-\>symbol("model/model.dae"); ```


Also, all geometry, textures, material and effects needed by your model is automaticly added to the assetLibrary. So, if you know the name of one of them you can have a access throw the `AssetLibrary::texture(name)`, `AssetLibrary::geometry(name)`, `AssetLibrary::material(name)` and `AssetLibrary::effect(name)` methods.

Use default Effect
------------------

Most of the time, your model does not know the effect that its surfaces are supposed to be linked with. In order to indicate an effect, you must use the defaultOptions of the `AssetLibrary`.

\<source lang="cpp\> sceneManager-\>assets()-\>defaultOptions()-\>effect(sceneManager-\>assets()-\>effect(DEFAULT\EFFECT)); ```


You can also choose a default material

```
 sceneManager-\>assets()-\>defaultOptions()-\>material()-\>set("diffuseColor", Vector4::create(0.8f, 0.1f, 0.1f, 1.0f)); ```


Final Code
----------

```


1.  include "minko/Minko.hpp"
2.  include "minko/MinkoSDL.hpp"
3.  include "minko/MinkoASSIMP.hpp"
4.  include "minko/MinkoJPEG.hpp"

using namespace minko; using namespace minko::component; using namespace minko::math;

const uint WINDOW\WIDTH = 800; const uint WINDOW\HEIGHT = 600;

const std::string OBJ\MODEL\FILENAME = "model/pirate.obj"; const std::string DAE\MODEL\FILENAME = "model/pirate.dae";

int main(int argc, char\*\* argv) {

`   auto canvas = Canvas::create("Minko Tutorial - Load 3D files", WINDOW_WIDTH, WINDOW_HEIGHT);`
`   auto sceneManager = SceneManager::create(canvas->context());`

`   // setup assets`
`   sceneManager->assets()`
`       ->registerParser<`[`file::ASSIMPParser>`](file::ASSIMPParser>)`("obj")`
`       ->registerParser<`[`file::ASSIMPParser>`](file::ASSIMPParser>)`("dae")`
`       ->registerParser<`[`file::JPEGParser>`](file::JPEGParser>)`("jpg");`

`   sceneManager->assets()->load("effect/Basic.effect");`
`   `
`   // add the model to the asset list`
`   sceneManager->assets()->queue(OBJ_MODEL_FILENAME);`
`   sceneManager->assets()->queue(DAE_MODEL_FILENAME);`

`   sceneManager->assets()->defaultOptions()->generateMipmaps(true);`
`   sceneManager->assets()->defaultOptions()->effect(sceneManager->assets()->effect("effect/Basic.effect"));`

`   auto complete = sceneManager->assets()->complete()->connect([&](file::AssetLibrary::Ptr assets)`
`   {`
`       auto root = scene::Node::create("root")->addComponent(sceneManager);`

`       auto camera = scene::Node::create("camera")`
`           ->addComponent(Renderer::create(0x7f7f7fff))`
`           ->addComponent(Transform::create(`
`           Matrix4x4::create()->lookAt(Vector3::create(0.f, 0.f, 0.f), Vector3::create(0.f, 0.f, 5.f))`
`           ))`
`           ->addComponent(PerspectiveCamera::create(`
`           (float) WINDOW_WIDTH / (float) WINDOW_HEIGHT, (float) PI * 0.25f, .1f, 1000.f)`
`           );`
`       root->addChild(camera);`

`       auto objModel = assets->symbol(OBJ_MODEL_FILENAME);`
`       auto daeModel = assets->symbol(DAE_MODEL_FILENAME);`

`       // change scale for the obj file`
`       objModel->component<Transform>()->matrix()->appendScale(0.01f);`

`       // change position`
`       objModel->component<Transform>()->matrix()->translation(-1.f, -1.f, 0.f);`
`       daeModel->component<Transform>()->matrix()->translation(1.f, -1.f, 0.f);`

`       // add to the scene`
`       root->addChild(objModel);`
`       root->addChild(daeModel);`

`       auto enterFrame = canvas->enterFrame()->connect([&](Canvas::Ptr canvas, float t, float dt)`
`       {`
`           sceneManager->nextFrame(t, dt);`
`       });`

`       canvas->run();`
`   });`

`   sceneManager->assets()->load();`

`   return 0;`

} ```


<Category:Tutorials>

