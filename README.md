# FidelityFX CAS (Contrast Adaptive Sharpening) v1.0

Copyright (c) 2020 Advanced Micro Devices, Inc. All rights reserved.
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:
The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.

## Contrast Adaptive Sharpening (CAS)

Contrast Adaptive Sharpening (CAS) is a low overhead adaptive sharpening algorithm with optional up-sampling. The technique is developed by Timothy Lottes (creator of FXAA) and was created to provide natural sharpness without artifacts. This directory contains the source code for CAS as well as samples demonstrating the technique (with source). The directory structure is as follows:

- [sample](sample) contains the source code for the above 2 CAS samples
- media is a submodule which contains the art assets for the above CAS samples
- [ffx-cas](ffx-cas) contains the headers that implement the CAS algorithm

You can find the binaries for CAS in the [releases](https://github.com/GPUOpen-Effects/FidelityFX-CAS/releases) section on GitHub.

## Build Instructions

The CAS samples are written in C++ and require CMake and Visual Studio to be built. To build the samples, follow the below steps:

 - Run [sample\build\GenerateSolutions.bat](sample/build/GenerateSolutions.bat) which creates the `sample\build\DX12` and `sample\build\VK` folders
 - Go into `sample\build\DX12` or `sample\build\VK` and open the `CAS_Sample_DX12\VK.sln` files
 - Build the project and run it (you should see a 3D helmet).

## Running Instructions

When running the samples, you can use the below options to test different configurations of CAS:

 - You can make the demo full screen via `Alt+Enter`. You can set the render resolution which decides how much CAS will have to upscale the image when CAS is enabled (without enabling, it’s a naïve upscale). The GUI will also let you choose different CAS modes (sharpen only or up-sample) with packed and unpacked versions.
 - You can use the `q`, `w` and `e` keys to set different CAS modes. `q` sets it to no CAS, `w` sets it to up-sampling, and `e` sets it to sharpen only.
 - The code implementing CAS can be found in FFX_CAS\cas-samples\src

You can find the documentation for the CAS algorithm and how to implement it using the FFX CAS headers at [ffx-cas\ffx_cas.h](ffx-cas/ffx_cas.h).

## Command Line Tool

There is also a command line tool to allow you to test the effects of FidelityFX CAS on standalone image files such as screenshots from your game, allowing you to evaluate it before integration. Please see the [FidelityFX-CLI](https://github.com/GPUOpen-Effects/FidelityFX-CLI) project for more details.

## How to use this project with CMAKE

Here is an example of using this project with cmake using the following structure

```tree
.
├── CMakeLists.txt
├── include
└── src
    └── main.cpp
```

CMakeLists.txt
```cmake
cmake_minimum_required(VERSION 3.22)
project(fidelifyfx-cas-baseproject VERSION 0.1)

include(FetchContent)

FetchContent_Declare(
  ffx-cas
  GIT_REPOSITORY https://github.com/arthurafarias/FidelityFX-CAS.git
  GIT_TAG        3a89494e45ccac621fbf10c8f72a62fc0c182d8b
)

FetchContent_MakeAvailable(ffx-cas)

add_executable(${PROJECT_NAME} src/main.cpp)

target_include_directories(${PROJECT_NAME} PUBLIC ${ffx-cas_SOURCE_DIR})
```

src/main.c
```c
#include "ffx-cas/ffx_a.h"

int main(int argc, char* argv[])
{
    return 0;
}
```