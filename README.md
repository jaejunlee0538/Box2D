Box2D is a 2D physics engine for games.

For help with Box2D, please visit http://www.box2d.org. There is a forum there where you may post your questions.

Please see Building.txt to learn how to build Box2D and run the testbed.

To run the demos, set "Testbed" as your startup project and press F5. Some test bed commands are:
- 'r' to reset the current test
- SPACE to launch a bomb
- arrow keys to pan
- 'x' and 'z' to zoom in/out
- use the mouse to click and drag objects

Erin Catto
http://www.box2d.org

---------------------------
## Building on Ubuntu 14.04.02 x64

**I couldn't use `glfw` which included with Box2D repo.**

I had to install latest `glfw3` and `glew` by my-self and remove dependencies of `Testbed` to `glew` and `glfw` which are included in Box2D Package.

**You may have to install additional libraries.**

You have to add include directory and target link library in `TestBed/CMakeLists.txt` like the following.

```cmake
include_directories (
	${GLEW_INCLUDE_DIRS}
	${GLFW_INCLUDE_DIRS}
  ...
)

target_link_libraries (
  ...
	${GLEW_LIBRARIES}
	${GLFW_LIBRARIES}
  ...
	X11 Xrandr Xi Xxf86vm Xcursor Xinerama
	pthread
)
```

Now we have to include external headers files for `glew` and `glfw`. But in my case the path in which those headers are installed was not compatible with `Testbed`'s source codes, few `#include` modifications were required.

* `<glew/glew.h>` changed to `<GL/glew.h>`
* `<glfw/glfw3.h>` changed to `<GLFW/glfw3.h>`

That's all. Now you may be able to build `Testbed` executable.

If you have **shader-related** runtime-error, try installing **proprietary graphic driver**.

In my case `GLSL 4.0.0 is not supported.` was shown and resolved by installing **NVIDIA binary driver - version 346.82**.
