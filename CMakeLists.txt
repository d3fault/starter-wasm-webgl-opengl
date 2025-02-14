cmake_minimum_required(VERSION 3.0)

# If the EMSDK environment variable is set, configure the toolchain file. this has to be done before the project(demo) line below
if(DEFINED ENV{EMSDK})
    set(CMAKE_TOOLCHAIN_FILE "$ENV{EMSDK}/upstream/emscripten/cmake/Modules/Platform/Emscripten.cmake" CACHE STRING "Emscripten toolchain file")
    message(STATUS "WebAssembly build enabled")
    message(STATUS "CMAKE_TOOLCHAIN_FILE='${CMAKE_TOOLCHAIN_FILE}'")
else()
    message(STATUS "WebAssembly build NOT enabled. EMSDK environment variable is not set. Falling back to native build. If you want to compile for WebAssembly, first `source emsdk_env.sh` in the emsdk directory")
endif()

project(demo)

add_definitions(-std=c++14)
set(CMAKE_CXX_STANDARD 14)

if(NOT DEFINED ENV{EMSDK})
    set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "Build GLFW examples" FORCE)
    find_package(glfw3 REQUIRED) # Locate the system-installed GLFW3
    find_package(OpenGL REQUIRED) # OpenGL is needed for GLFW
endif()

# Source files
set(DEMO_SOURCE src/demo.cpp)

# Build target
add_executable(demoapp ${DEMO_SOURCE})

if(DEFINED ENV{EMSDK})
    set_target_properties(demoapp
        PROPERTIES SUFFIX ".html"
        LINK_FLAGS "-Os -s USE_WEBGL2=1 -s FULL_ES3=1 -s USE_GLFW=3 -s WASM=1")
else()
    # Link against GLFW and OpenGL for native builds
    target_link_libraries(demoapp glfw OpenGL::GL)
endif()
