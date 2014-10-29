Creating the material
---------------------

To create a `phongMaterial`, we simply call `material::PhongMaterial::create` method that returns a `material::PhongMaterial::Ptr`.


```cpp
 auto phongMaterial = material::PhongMaterial::create(); 
```


You'll find more information about the `phongMaterial` in this tutorial [Working with the PhongMaterial](Working_with_the_PhongMaterial.md)

Properties of the phong material
--------------------------------

We'll show the different properties of the `phongMaterial` on three different scenes.

Each set of properties has a dedicated tutorial in the **tutorials** section:

-   [Working with the PhongMaterial](Working_with_the_PhongMaterial.md), to create a PhongMaterial then change the `diffuseColor`, `diffuseMap`, `specularColor` and the `shininess`
-   [[Working with normal maps | Working with normal maps]
-   [ Working with specular maps](Working_with_specular_maps_.md)
-   [ Working with environment maps](Working_with_environment_maps_.md)

The `phongMaterial` has access to a `diffuseColor` and a `diffuseMap`. Those properties can be set in the same way than the `basicMaterial` ([Working with the BasicMaterial](Working_with_the_BasicMaterial.md)).

| Right                                                                  | Left                                                     | Front                                                      |
|------------------------------------------------------------------------|----------------------------------------------------------|------------------------------------------------------------|
| ![](images/InitSceneDirectional.png "images/InitSceneDirectional.png") | ![](images/InitSceneSpot.png "images/InitSceneSpot.png") | ![](images/InitScenePoint.png "images/InitScenePoint.png") |

### Specular Color

Specular color is the color of the light specular reflection. The default value is white.

<source lang="cpp\> phongMaterial->specularColor(0xFF0000FF); 
```


| specular color | Right                                                      | Left                                                       | Front                                                      |
|----------------|------------------------------------------------------------|------------------------------------------------------------|------------------------------------------------------------|
| 0xFF0000FF     | ![](images/RedSpecular1.PNG "images/RedSpecular1.PNG")     | ![](images/RedSpecular2.PNG "images/RedSpecular2.PNG")     | ![](images/RedSpecular3.PNG "images/RedSpecular3.PNG")     |
| 0xC0FFC0FF     | ![](images/GreenSpecular1.PNG "images/GreenSpecular1.PNG") | ![](images/GreenSpecular2.PNG "images/GreenSpecular2.PNG") | ![](images/GreenSpecular3.PNG "images/GreenSpecular3.PNG") |

To have more information about specular color : [Working with the PhongMaterial](Working_with_the_PhongMaterial.md)

### Shininess

Empirically, the shininess parameter controls how sharp specular reflections will look across the surface of the object. The default value is 8.


```cpp
 phongMaterial->shininess(32.f); 
```


| shininess | Right                                                    | Left                                                     | Front                                                    |
|-----------|----------------------------------------------------------|----------------------------------------------------------|----------------------------------------------------------|
| 2         | ![](images/Shiniess0_2_1.PNG "images/Shiniess0_2_1.PNG") | ![](images/Shiniess0_2_2.PNG "images/Shiniess0_2_2.PNG") | ![](images/Shiniess0_2_3.PNG "images/Shiniess0_2_3.PNG") |
| 16        | ![](images/Shiniess16_1.PNG "images/Shiniess16_1.PNG")   | ![](images/Shiniess16_2.PNG "images/Shiniess16_2.PNG")   | ![](images/Shiniess16_3.PNG "images/Shiniess16_3.PNG")   |
| 64        | ![](images/Shiniess64_1.PNG "images/Shiniess64_1.PNG")   | ![](images/Shiniess64_2.PNG "images/Shiniess64_2.PNG")   | ![](images/Shiniess64_3.PNG "images/Shiniess64_3.PNG")   |

To have more information about shininess : [Working with the PhongMaterial](Working_with_the_PhongMaterial.md)

### Environment Map & Environment Alpha

The environment alpha indicates the percentage of environment map that should be mixed with the computed color. The environment map is a texture that represents the environment around your scene.


```cpp
 // first of all, we need a environment map. We add a new asset to the loading queue.

sceneManager->assets()->queue("texture/envmap.png");

// when all assets are loaded

phongMaterial->environmentMap(assets->texture("texture/envmap.png"), render::EnvironmentMap2dType::BlinnNewell); phongMaterial->environmentAlpha(0.2f); 
```


| Environment Alpha                                        | 0.2                                          | 0.5                                          | 0.95                                         |
|----------------------------------------------------------|----------------------------------------------|----------------------------------------------|----------------------------------------------|
| ![](images/Ditchriverii9.jpg "images/Ditchriverii9.jpg") | ![](images/Envmap1.PNG "images/Envmap1.PNG") | ![](images/Envmap2.PNG "images/Envmap2.PNG") | ![](images/Envmap3.PNG "images/Envmap3.PNG") |

If you need more information about environment map : [ Working with environment maps](Working_with_environment_maps_.md)

### Normal Map


```cpp
 // first of all, we need a normal map. We add a new asset to the loading queue.

sceneManager->assets()->queue("texture/normalmap.png");

// when all assets are loaded in the handler function of assets->complete()

phongMaterial->normalMap(assets->texture("texture/normalmap.png")); 
```


| scope="col" widt"100px"| DiffuseMap / NormalMap            | Right                                            | Left                                             | Front                                            |
|------------------------------------------------------------|--------------------------------------------------|--------------------------------------------------|--------------------------------------------------|
| ![ link=](images/TextureNormal1.jpg " link=")              | ![](images/Normal1_1.PNG "images/Normal1_1.PNG") | ![](images/Normal1_2.PNG "images/Normal1_2.PNG") | ![](images/Normal1_3.PNG "images/Normal1_3.PNG") |
| ![ link=](images/TextureNormal2.jpg " link=")              | ![](images/Normal2_1.PNG "images/Normal2_1.PNG") | ![](images/Normal2_2.PNG "images/Normal2_2.PNG") | ![](images/Normal2_3.PNG "images/Normal2_3.PNG") |
| ![](images/TextureNormal3.jpg "images/TextureNormal3.jpg") | ![](images/Normal3_1.PNG "images/Normal3_1.PNG") | ![](images/Normal3_2.PNG "images/Normal3_2.PNG") | ![](images/Normal3_3.PNG "images/Normal3_3.PNG") |
||

If you need more information about normal mapping : [Working with normal maps](Working_with_normal_maps_.md)

### Specular Map


```cpp
 phongMaterial->shininess(2); phongMaterial->specularMap(assets->texture("texture/specularmap.png")); 
```


| scope="col" widt"100px"| DiffuseMap / SpecularMap              | Right                                                      | Left                                                       | Front                                                      |
|----------------------------------------------------------------|------------------------------------------------------------|------------------------------------------------------------|------------------------------------------------------------|
| ![ link=](images/Texturespecular1.jpg " link=")                | ![](images/SpecularMap1_1.PNG "images/SpecularMap1_1.PNG") | ![](images/SpecularMap1_2.PNG "images/SpecularMap1_2.PNG") | ![](images/SpecularMap1_3.PNG "images/SpecularMap1_3.PNG") |
| ![ link=](images/Texturespecular22.jpg " link=")               | ![](images/SpecularMap2_1.PNG "images/SpecularMap2_1.PNG") | ![](images/SpecularMap2_2.PNG "images/SpecularMap2_2.PNG") | ![](images/SpecularMap2_3.PNG "images/SpecularMap2_3.PNG") |
| ![](images/Texturespecular3.jpg "images/Texturespecular3.jpg") | ![](images/SpecularMap3_1.PNG "images/SpecularMap3_1.PNG") | ![](images/SpecularMap3_2.PNG "images/SpecularMap3_2.PNG") | ![](images/SpecularMap3_3.PNG "images/SpecularMap3_3.PNG") |
||

If you need more information about specular maps : [ Working with specular maps](Working_with_specular_maps_.md)

Full Example
------------


```cpp
 #include "minko/Minko.hpp" #include "minko/MinkoPNG.hpp" #include "minko/MinkoSDL.hpp"

using namespace minko; using namespace minko::component; using namespace minko::math;

int main(int argc, char** argv) {

`   auto canvas = Canvas::create("My title", 800, 600);`

`   auto sceneManager = SceneManager::create(canvas->context());`

`   // setup assets`
`   sceneManager->assets()->defaultOptions()->resizeSmoothly(true);`
`   sceneManager->assets()->defaultOptions()->generateMipmaps(true);`
`   sceneManager->assets()`
`   ->registerParser<`[`file::PNGParser>`](file::PNGParser>)`("png")`
`   ->queue("texture/diffuse.png")`
`   ->queue("texture/envmap.png")`
`   ->queue("texture/normal.png")`
`   ->queue("texture/specular.png")`
`   ->queue("effect/Phong.effect");`

`   auto _ = sceneManager->assets()->complete()->connect([=](file::AssetLibrary::Ptr assets)`
`   {`
`   auto phongMaterial = material::PhongMaterial::create()->diffuseColor(math::Vector4::create(1., 1., 1., 1.));`
`   auto root = scene::Node::create("root")->addComponent(sceneManager);`

`   phongMaterial->shininess(2);`
`   phongMaterial->diffuseMap(assets->texture("texture/diffuse.png"));`
`   phongMaterial->normalMap(assets->texture("texture/normal.png"));`
`   phongMaterial->specularMap(assets->texture("texture/specular.png"));`
`   phongMaterial->specularColor(0xC0FFC0FF);`
`   phongMaterial->environmentMap(assets->texture("texture/envmap.png"), render::EnvironmentMap2dType::BlinnNewell);`
`   phongMaterial->environmentAlpha(0.15);`
`       `
`   auto camera = scene::Node::create("camera")`
`       ->addComponent(Renderer::create(0x00000000))`
`       ->addComponent(Transform::create(Matrix4x4::create()->lookAt(Vector3::create(0.0f, 0.f, 0.f), Vector3::create(0.0f, 1.f, 1.3f))`
`           ))`
`       ->addComponent(PerspectiveCamera::create(800.f / 600.f, (float)PI * 0.25f, .1f, 1000.f));`
`   `
`       root->addChild(camera);`

`   auto mesh = scene::Node::create("mesh")`
`       ->addComponent(Transform::create(Matrix4x4::create()))`
`       ->addComponent(`
`                   Surface::create(geometry::SphereGeometry::create(sceneManager->assets()->context(), 30, 30, true),`
`           phongMaterial,`
`           assets->effect("effect/Phong.effect")`
`   ));`

`   root->addChild(mesh);`

`   auto spotLight = scene::Node::create("SpotLight")`
`       ->addComponent(SpotLight::create(0.6f, 0.78f, 20.f))`
`       ->addComponent(Transform::create(Matrix4x4::create()->lookAt(Vector3::zero(), Vector3::create(3.f, 5.f, 1.5f))));`

`   spotLight->component<SpotLight>()->diffuse(1.4f);`
`   spotLight->component<SpotLight>()->specular(2);`

`   auto enterFrame = canvas->enterFrame()->connect([&](Canvas::Ptr canvas, uint time, uint deltaTime)`
`   {`
`       sceneManager->nextFrame();`
`   });`

`   canvas->run();`
`   });`

`   sceneManager->assets()->load();`

`   return 0;`

} 
```


|----------------------------------------------------------|--------------------------------------------------------|--------------------------------------------------------|
| ![](images/FinalResult11.PNG "images/FinalResult11.PNG") | ![](images/FinalResult2.PNG "images/FinalResult2.PNG") | ![](images/FinalResult3.PNG "images/FinalResult3.PNG") |


