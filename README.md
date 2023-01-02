# CMake Cookbook

按照 [CMake菜谱（CMake Cookbook中文版）](https://www.bookstack.cn/read/CMake-Cookbook/README.md)一步步学习 CMake

## 实验环境
```sh
# 使用 docker 镜像
docker run -v $my_repo:/home/mightybuilder/CMakeCookbook -it devcafe/cmake-cookbook_ubuntu-18.04
```

## ch01

### 1.1 将单个源文件编译为可执行文件

设置 cmake 最小版本以及项目名称
```cmake
cmake_minimum_required(VERSION 3.5 FATAL_ERROR)
project(recipe01 LANGUAGES CXX)
```

通过编译和链接源文件 `main.cpp` 生成可执行文件 `hello`
```Cmake
# CMakeLists.txt
add_executable(hello main.cpp)
```
进行构建
```sh
mkdir build
cd build
cmake ..
# 或者直接
cmake -H. -Bbuild
make .
```
`-H` 指定了查找 CMakeLists.txt 的目录，`-B` 指定了生成目录。
CMake 默认生成 Unix Makefile，然后通过 `make` 或者 `cmake --build .` 命令根据其来构建项目。 

### 1.2 切换生成器

使用 `-G` 指定 Generator
```sh
# 先清理 build 下的文件
# Either remove the CMakeCache.txt file and CMakeFiles directory or choose a different binary directory.
cmake -G Ninja ..
cmake --build .
```
build.ninja 和 rules.ninja 为 Ninja 的生成的构建语句和构建规则，然后通过 `cmake --build` 根据上述文件来构建项目。

    cmake --build . 将 ninja 命令封装在一个跨平台的接口中。

### 1.3 构建和链接静态库和共享库

**静态库**在编译期间已经**由编译器与链接器将它集成至应用程序内**，并制作成目标文件以及可以独立运作的可执行文件。

**共享库**，进行动态链接，在可执行文件装载时或运行时，才由操作系统的装载程序进行加载。

创建静态库，`add_library` 将指定的源码编译到库中，`target_link_libraries` 将库链接到可执行文件。
```cmake
add_library(message
  STATIC
    Message.hpp
    Message.cpp
  )
target_link_libraries(hello message)
```
`add_library` 的第二个参数常用值：

    STATIC：用于创建静态库，即编译文件的打包存档，以便在链接其他目标时使用，例如：可执行文件。
    SHARED：用于创建动态库，即可以动态链接，并在运行时加载的库。可以在CMakeLists.txt中使用add_library(message SHARED Message.hpp Message.cpp)从静态库切换到动态共享对象(DSO)。
    OBJECT：可将给定add_library的列表中的源码编译到目标文件，不将它们归档到静态库中，也不能将它们链接到共享对象中。如果需要一次性创建静态库和动态库，那么使用对象库尤其有用。我们将在本示例中演示。
    MODULE：又为DSO组。与SHARED库不同，它们不链接到项目中的任何目标，不过可以进行动态加载。该参数可以用于构建运行时插件。

创建静态库和共享库
```cmake
add_library(message-objs
  OBJECT
      Message.hpp
      Message.cpp
  )
add_library(message-shared
  SHARED
      $<TARGET_OBJECTS:message-objs>
  )
set_target_properties(message-shared
    PROPERTIES
        OUTPUT_NAME "message"
    )
add_library(message-static
  STATIC
      $<TARGET_OBJECTS:message-objs>
  )
set_target_properties(message-static
    PROPERTIES
        OUTPUT_NAME "message"
    )
target_link_libraries(hello message-static)
```
最终得到两个文件 libmessage-shared.so 和 libmessage-static.a

### 1.4 用条件句控制编译
