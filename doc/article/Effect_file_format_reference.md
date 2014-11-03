Effect File Format
==================

Effect files (*.effect) are JSON formated text files used to describe rendering effects.

Default Bindings
----------------

There are three types of bindings:

-   **attribute bindings** are used to bind vertex shader attribute properties;
-   **uniform bindings** are used to bind vertex/fragment shader uniform properties;
-   **state bindings** are used to bind passes rendering states.

Bindings are used to declare how each property of each pass of the effect will be bound to a property available in the node <data::Container> object.

```javascript
"attributeBindings" : {

   "position"      : "geometry/vertex/attribute/position"

},

"uniformBindings" : {

   "diffuseColor"      : "material/diffuse/rgba",
   "modelToWorldMatrix"    : "transform/modelToWorldMatrix",
   "worldToScreenMatrix"   : "transform/worldToScreenMatrix"

},

"stateBindings" : {

   "blendMode"     : "material/blendMode",
   "depthTest"     : "material/depthTest"

} 
```


The bindings declared in the root effect node are considered "default" bindings: they will apply for all passes. But each pass can declare its own bindings and eventually replace the default ones (see [](../tutorial/#Pass_Bindings.md)).

Passes
------

Each effect can have multiple passes. Each pass has:

-   a name (optional)
-   bindings (optional)
-   rendering states (optional)
-   a vertex shader
-   a fragment shader

### Name

The name of the rendering pass. Names can be used to declare passes that can be used across multiple effects.

### Pass Bindings

Each pass can re-declare attribute, uniform and state bindings. The goal is to be able to have different binding values for a property that might have the same name among different passes. The blending state is a good example:

```javascript
// some effect {

   // by default, the "blendMode" state is bound to the "material/blendMode" property
   "stateBindings"     : {
       "blendMode" : "material/blendMode"
   },

   "passes" : [{
       "name"  : "first pass",
       // "first pass" doest no re-declare the "blendMode" state binding: it will use
       // the default one
       // ...
   },
   {
       "name"  : "second pass",
       // "second pass" re-declare the "blendMode" state binding: it will *not* use
       // the default one
       "stateBindings"     : {
           "blendMode" : "some/other/blendMode/property"
       },
       // ...
   }]

} 
```


### Rendering States

| Name | Type | Description | Example |
|------|------|-------------|---------|
| priority  | float   | The priority of the render pass: passes with higher priority are rendered first. | "priority" : 42.5|

| blendMode | array[string, string] or string | less | "blendMode" : ["one", "zero"] "blendMode" : "default"| 

| depthTest | array[boolean, string]   | less | "depthTest" : [true, "less"] |

Here is an example that will set the first pass rendering states:

```javascript
"passes" : [{

   "priority"  : 0,
   "blendMode" : ["one", "zero"],
   "depthTest" : [false, "less"],

// ... 
```


### Vertex Shader

The GLSL code for the vertex shader.

Example: 
```javascript
"vertexShader" : "

   attribute vec3 position;

  
uniform mat4 modelToWorldMatrix;
  
uniform mat4 worldToScreenMatrix;

   void main(void)
   {
       gl_Position =  worldToScreenMatrix * modelToWorldMatrix * vec4(position, 1.0);
   }

" 
```


### Fragment Shader

The GLSL code for the fragment shader.

Example: 
```javascript
"fragmentShader" : "

   uniform vec4 diffuseColor;

   void main(void)
   {
       gl_FragColor = diffuseColor;
   }

" 
```


Complete Example
----------------

```javascript
// basic effect {

   "name"  : "basic",
   
   "attributeBindings" : {
       "position"      : "geometry/vertex/attribute/position"
   },
   
   "uniformBindings"   : {
       "diffuseColor"      : "material/diffuse/rgba",
       "modelToWorldMatrix"    : "transform/modelToWorldMatrix",
       "worldToScreenMatrix"   : "transform/worldToScreenMatrix"
   },
   
   "stateBindings" : {
       "blendMode"     : "material/blendMode",
       "depthTest"     : "material/depthTest"
   },
   
   "passes"    : [{
       "priority"      : 0,
       "blendMode"     : ["one", "zero"],
       "depthTest"     : [false, "less"],
       "vertexShader"  : "
           attribute vec3 position;

          
uniform mat4 modelToWorldMatrix;
          
uniform mat4 worldToScreenMatrix;

           void main(void)
           {
               gl_Position =  worldToScreenMatrix * modelToWorldMatrix * vec4(position, 1.0);
           }
       ",
       "fragmentShader"    : "
           uniform vec4 diffuseColor;

           void main(void)
           {
               gl_FragColor = diffuseColor;
           }
       "
   }]

} 
```


