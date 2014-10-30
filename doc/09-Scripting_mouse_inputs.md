Introduction to mouse inputs
----------------------------

The following section introduces the two different ways to deal with mouse inputs (or any kind of interactions based on signals for that matter): signals callbacks and coroutines. You are free to choose one or the other according to the situation.

### Listening to mouse signals


```lua
 -- my\mouse\script.lua function my\mouse\script:start(node)

localmouse=getCanvas().mouse

mouse.leftButtonDown:connect(function(m)print('leftbuttondown!')end)
mouse.leftButtonUp:connect(function(m)print('leftbuttonup!')end)
mouse.move:connect(function(m,dx,dy)print('mousemove!')end)

end 
```


### Alternative: Waiting for mouse signals

Coroutines are a great way to work with an asynchronous API using a synchronous syntax. Instead of listening to a specific signal and act accordingly in the corresponding callback, we will simply pause the script and wait for "something to happen" before resuming.

The following code will "wait" for the mouse.leftButtonDown signal before continuing:


```lua
 function my\mouse\script:start(node)

self.co=coroutine.create(my_mouse_script.handleMouseDown)
coroutine.resume(self.co,self)

end

function my\mouse\script:handleMouseDown()

print("pleaseclick...")
--executionofthisspecificscriptwillpausewhenithitsthecalltowait()
wait(getCanvas().mouse.leftButtonDown)
--executionwillresumeherewhenthemouse.leftButtonDownhasbeenexecuted
print("leftbuttondown!")

end 
```


Final code
----------


```cpp
 #include "minko/Minko.hpp" #include "minko/MinkoSDL.hpp" #include "minko/MinkoLua.hpp"

using namespace minko; using namespace minko::math; using namespace minko::component;

const uint WINDOW\WIDTH = 800; const uint WINDOW\HEIGHT = 600;

int main(int argc, char** argv) {

autocanvas=Canvas::create("MinkoTutorial-Scriptingmouseinputs",WINDOW_WIDTH,WINDOW_HEIGHT);
autosceneManager=component::SceneManager::create(canvas->context());
autoroot=scene::Node::create("root")->addComponent(sceneManager);

//initializationofLuacontext
LuaContext::initialize(argc,argv,root,canvas);

//addaLuaScriptManagertotherootnode
root->addComponent(LuaScriptManager::create());

sceneManager->assets()->registerParser<[file::LuaScriptParser>](file::LuaScriptParser>)("lua");
sceneManager->assets()->queue("script/my_mouse_script.lua");

autocomplete=sceneManager->assets()->complete()->connect([&](file::AssetLibrary::Ptrassets)
{
root->addComponent(assets->script("script/my_mouse_script.lua"));

autoenterFrame=canvas->enterFrame()->connect([&](Canvas::Ptrc,floatt,floatdt)
{
sceneManager->nextFrame(t,dt);
});

canvas->run();
});

//actuallybeginloadingoperations
sceneManager->assets()->load();

return0;

} 
```


