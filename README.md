# WebAssembly/WebGL and Native/OpenGL 3D project StarterKit

A starting point for a new web and native cross-platform 3D project.

Builds with CMake. Uses [GLFW](http://www.glfw.org/).

## Details

* Requires `CMake` and `GLFW` installed.
* Displays an empty green window. Nothing else.

## Building

### WebAssembly

* [Download or Compile the WASM Toolchain][wasm-toolchain].
* Setup the WASM toolchain
  * `git clone https://github.com/emscripten-core/emsdk.git`
  * `cd emsdk`
  * `./emsdk install latest`
  * `./emsdk activate latest`
  * `source ./emsdk_env.sh`
* Build/Run the example
  * `cd starter-wasm-webgl-opengl`
  * `mkdir buildwasm && cd buildwasm`
  * `cmake ..`
  * `cmake --build .`
  * `python -m SimpleHTTPServer 8080 #or other webserver`
  * Available at: http://localhost:8080/demoapp.html

[wasm-toolchain]:http://webassembly.org/getting-started/developers-guide/

### Native Linux

Tested on Debian 11.

* Install development tools X11 and OpenGL: `sudo apt install xorg-dev libgl1-mesa-dev libglfw3-dev`
* Build/Run the example
  * `cd starter-wasm-webgl-opengl`
  * `mkdir buildnative && cd buildnative`
  * `cmake ..`
  * `cmake --build .`
  * `./demoapp`

Thanks to:

* https://cmake.org/cmake/help/v3.0/
* http://www.glfw.org/docs/latest/quick.html
* https://github.com/HarryLovesCode/WebAssembly-WebGL-2
* https://github.com/daminetreg/emscripten-example/

## Todo

* Test/debug on a fresh Ubuntu install
* Native MacOS
* Native Windows
* More polish
