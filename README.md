# Hello, CMake

按照 [CMake 菜谱](https://www.bookstack.cn/read/CMake-Cookbook/README.md)、[Modern CMake](https://modern-cmake-cn.github.io/Modern-CMake-zh_CN/) 和 [Useful CMake Examples](https://github.com/ttroy50/cmake-examples) 一步步学习如何使用 CMake 以及 C/C++ 的编译。

*   [Hello, CMake](#hello-cmake)
*   [实验环境](#%E5%AE%9E%E9%AA%8C%E7%8E%AF%E5%A2%83)
*   [起步](#%E8%B5%B7%E6%AD%A5)
    *   [设置最低版本要求](#%E8%AE%BE%E7%BD%AE%E6%9C%80%E4%BD%8E%E7%89%88%E6%9C%AC%E8%A6%81%E6%B1%82)
    *   [设置项目](#%E8%AE%BE%E7%BD%AE%E9%A1%B9%E7%9B%AE)
    *   [将单个源文件编译为可执行文件](#%E5%B0%86%E5%8D%95%E4%B8%AA%E6%BA%90%E6%96%87%E4%BB%B6%E7%BC%96%E8%AF%91%E4%B8%BA%E5%8F%AF%E6%89%A7%E8%A1%8C%E6%96%87%E4%BB%B6)
    *   [切换生成器](#%E5%88%87%E6%8D%A2%E7%94%9F%E6%88%90%E5%99%A8)
    *   [生成库和链接到目标](#%E7%94%9F%E6%88%90%E5%BA%93%E5%92%8C%E9%93%BE%E6%8E%A5%E5%88%B0%E7%9B%AE%E6%A0%87)
    *   [构建和链接静态库和共享库](#%E6%9E%84%E5%BB%BA%E5%92%8C%E9%93%BE%E6%8E%A5%E9%9D%99%E6%80%81%E5%BA%93%E5%92%8C%E5%85%B1%E4%BA%AB%E5%BA%93)
*   [CMake 变量、语句和函数](#cmake-%E5%8F%98%E9%87%8F%E8%AF%AD%E5%8F%A5%E5%92%8C%E5%87%BD%E6%95%B0)
    *   [变量](#%E5%8F%98%E9%87%8F)
        *   [缓存变量](#%E7%BC%93%E5%AD%98%E5%8F%98%E9%87%8F)
        *   [环境变量](#%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F)
    *   [缓存](#%E7%BC%93%E5%AD%98)
    *   [属性](#%E5%B1%9E%E6%80%A7)
    *   [条件语句](#%E6%9D%A1%E4%BB%B6%E8%AF%AD%E5%8F%A5)
    *   [循环语句](#%E5%BE%AA%E7%8E%AF%E8%AF%AD%E5%8F%A5)
    *   [生成器表达式](#%E7%94%9F%E6%88%90%E5%99%A8%E8%A1%A8%E8%BE%BE%E5%BC%8F)
    *   [函数](#%E5%87%BD%E6%95%B0)
        *   [函数参数](#%E5%87%BD%E6%95%B0%E5%8F%82%E6%95%B0)
    *   [调试 CMake](#%E8%B0%83%E8%AF%95-cmake)
*   [选项、配置、标志和外部环境](#%E9%80%89%E9%A1%B9%E9%85%8D%E7%BD%AE%E6%A0%87%E5%BF%97%E5%92%8C%E5%A4%96%E9%83%A8%E7%8E%AF%E5%A2%83)
    *   [选项](#%E9%80%89%E9%A1%B9)
    *   [指定编译器](#%E6%8C%87%E5%AE%9A%E7%BC%96%E8%AF%91%E5%99%A8)
    *   [文件](#%E6%96%87%E4%BB%B6)
        *   [configure\_file](#configure_file)
        *   [file](#file)
    *   [运行外部程序](#%E8%BF%90%E8%A1%8C%E5%A4%96%E9%83%A8%E7%A8%8B%E5%BA%8F)
    *   [自定义命令](#%E8%87%AA%E5%AE%9A%E4%B9%89%E5%91%BD%E4%BB%A4)
    *   [构建类型](#%E6%9E%84%E5%BB%BA%E7%B1%BB%E5%9E%8B)
    *   [编译选项](#%E7%BC%96%E8%AF%91%E9%80%89%E9%A1%B9)
    *   [目标属性](#%E7%9B%AE%E6%A0%87%E5%B1%9E%E6%80%A7)
    *   [操作系统类型](#%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F%E7%B1%BB%E5%9E%8B)
    *   [编译器类型](#%E7%BC%96%E8%AF%91%E5%99%A8%E7%B1%BB%E5%9E%8B)
    *   [处理器架构和指令集](#%E5%A4%84%E7%90%86%E5%99%A8%E6%9E%B6%E6%9E%84%E5%92%8C%E6%8C%87%E4%BB%A4%E9%9B%86)
*   [Git](#git)
    *   [git 子模块](#git-%E5%AD%90%E6%A8%A1%E5%9D%97)
    *   [获取 git commit id](#%E8%8E%B7%E5%8F%96-git-commit-id)
    *   [从 git 获取](#%E4%BB%8E-git-%E8%8E%B7%E5%8F%96)

# 实验环境

```sh
# 使用 docker 镜像
docker run -v $my_repo:/home/mightybuilder/CMakeCookbook -it devcafe/cmake-cookbook_ubuntu-18.04
```

或者

*   gcc version >= 7.3.0
*   GNU Make >= 4.1
*   cmake version >= 3.12

# 起步

## 设置最低版本要求

> cmake\_minimum\_required(VERSION &lt;min&gt;\[...\<policy\_max>] \[FATAL\_ERROR])

```cmake
cmake_minimum_required(VERSION 3.12..3.22)
cmake_minimum_required(VERSION 3.5 FATAL_ERROR)

if(${CMAKE_VERSION} VERSION_LESS 3.20)
    cmake_policy(VERSION ${CMAKE_MAJOR_VERSION}.${CMAKE_MINOR_VERSION})
endif()
```

2.4 之前使用 `FATAL_ERROR` 选项在版本过低时将会产生一个错误而不是警告，2.6 之后这个参数是被接受的，但是不管使不使用，版本过低时都会产生错误。

    CMake Error at CMakeLists.txt:1 (cmake_minimum_required):
      CMake 3.xx or higher is required.  You are running version 3.yy

`policy_max` 选项会影响 cmake\_policy 设置。示例中根据 `if` 中的条件当版本低于 3.20 时使用当前版本的策略，高于等于 3.20 小于等于 3.22 时使用 3.22 的策略，高于 3.22 时使用 3.22 的策略。

## 设置项目

```cmake
project(
    example VERSION 1.0
    DESCRIPTION "example"
    LANGUAGES CXX)
```

设置项目名称、项目版本、描述、使用的语言

## 将单个源文件编译为可执行文件

通过编译和链接源文件 `main.cpp` 生成可执行文件 `hello`

```cmake
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
# 然后
make
```

`-H` 指定了查找 CMakeLists.txt 的目录，`-B` 指定了生成目录。
CMake 默认生成 Unix Makefile，然后通过 `make` 或者 `cmake --build .` 命令根据其来构建项目。

## 切换生成器

使用 `-G` 指定 Generator

```sh
# 先清理 build 下的文件
# Either remove the CMakeCache.txt file and CMakeFiles directory or choose a different binary directory.
cmake -G Ninja ..
cmake --build .
```

build.ninja 和 rules.ninja 为 Ninja 的生成的构建语句和构建规则，然后通过 `cmake --build` 根据上述文件来构建项目。

    cmake --build . 将 ninja 命令封装在一个跨平台的接口中。

## 生成库和链接到目标

通过 `add_library` 生成一个库

```cmake
add_library(one STATIC two.cpp three.h)
```

通过 `target_include_directories` 给目标添加目录

> target\_include\_directories(&lt;target&gt; \[SYSTEM] \[AFTER|BEFORE]
> \<INTERFACE|PUBLIC|PRIVATE> \[items1...]
> \[\<INTERFACE|PUBLIC|PRIVATE> \[items2...] ...])

```cmake
target_include_directories(one PUBLIC include)
```

通过 `target_link_libraries` 将目标和库链接起来

```cmake
target_link_libraries(another PUBLIC one)
```

## 构建和链接静态库和共享库

**静态库**在编译期间已经**由编译器与链接器将它集成至应用程序内**，并制作成目标文件以及可以独立运作的可执行文件。

**共享库**，进行动态链接，在可执行文件装载时或运行时，才由操作系统的装载程序进行加载。

创建静态库，`add_library` 将指定的源码编译到库中，`target_link_libraries` 将库链接到可执行文件。

```cmake
add_library(message STATIC Message.hpp Message.cpp)
target_link_libraries(hello message)
```

`add_library` 的第二个参数常用值：

> STATIC：用于创建静态库，即编译文件的打包存档，以便在链接其他目标时使用。
>
> SHARED：用于创建动态库，即可以动态链接，并在运行时加载的库。
>
> OBJECT：可将给定add\_library的列表中的源码编译到目标文件，不将它们归档到静态库中，也不能将它们链接到共享对象中。

**⚠   todo 具体什么是对象库？作用是什么**

参考：

*   [浅谈静态库和动态库](https://zhuanlan.zhihu.com/p/71372182)

创建静态库和共享库

```cmake
add_library(message-objs OBJECT Message.hpp Message.cpp)

add_library(message-shared SHARED $<TARGET_OBJECTS:message-objs> )
set_target_properties(message-shared PROPERTIES OUTPUT_NAME "message")

add_library(message-static STATIC $<TARGET_OBJECTS:message-objs>)
set_target_properties(message-static PROPERTIES OUTPUT_NAME "message")

target_link_libraries(hello message-static)
```

使用 `STATIC` 会得到 libmessage.a，使用 `SHARED` 会得到 libmessage.so，使用 `OBJECT` 两者都会产生。

# CMake 变量、语句和函数

## 变量

> set(&lt;variable&gt; &lt;value&gt;... \[PARENT\_SCOPE])

变量名通常使用大写，通过 `${}` 解析变量，变量自然有作用域的概念，使用 `PARENT_SCOPE` 选项变量将设置在当前的作用域上一层。

可以使用分隔符 `;` 将字符串的变量值分割成列表，或者使用 `list` 的子命令 `APPEND` 用于将元素挨个加入列表中。

```cmake
set(VAR1 "hello")
MESSAGE(STATUS "${VAR1}! CMake")
set(MY_LIST "one;two")
list(APPEND _sources Message.hpp Message.cpp)
```

变量的展开

```cmake
set(foo "bar")
set(bar "hello")
MESSAGE(STATUS "I am ${foo}")
MESSAGE(STATUS "${${foo}}")
```

### 缓存变量

首次申明后会被写入缓存中，修改后仍然读取的是缓存中的值。

```cmake
set(CACHE_VAR "lalala" CACHE STRING "Comment")
MESSAGE(STATUS "cache var ${CACHE_VAR}")
```

```txt
// CMakeCache.txt
//Comment
CACHE_VAR:STRING=lalala
```

### 环境变量

```cmake
set(ENV{variable_name} value)
$ENV{variable_name}
```

## 缓存

即 `CMakeCache.txt`，相关设置会缓存在这个文件中。

关于缓存的更多细节和用法：[CMake 缓存](https://cmake.org/cmake/help/book/mastering-cmake/chapter/CMake%20Cache.html)

## 属性

属性也可以赋值

```cmake
set_property(TARGET TargetName
             PROPERTY CXX_STANDARD 2a)
```

## 条件语句

在条件控制语句 `if(<constant|variable>)` 中

*   `1`， `ON`， `YES`， `TRUE`， `Y` 以及非零的数为 `true`
*   `0`， `OFF`， `NO`， `FALSE`， `N`， `IGNORE`， `NOTFOUND`， 空字符串，后缀 `-NOTFOUND` 为 `false`。

```cmake
if(<condition>)
  <commands>
elseif(<condition>) # optional block, can be repeated
  <commands>
else()              # optional block
  <commands>
endif()
```

条件中可以使用：

*   一元测试 `EXISTS`、`COMMAND`、和 `DEFINED`
*   二元测试 `EQUAL`、`LESS`、`LESS_EQUAL`、`GREATER`、`GREATER_EQUAL`、`STREQUAL`、`STRLESS`、`STRLESS_EQUAL`、`STRGREATER`、`STRGREATER_EQUAL`、`VERSION_EQUAL`、`VERSION_LESS`、`VERSION_LESS_EQUAL`、`VERSION_GREATER`、`VERSION_GREATER_EQUAL`、`PATH_EQUAL`、`MATCHES`
*   逻辑运算符 `NOT`、`AND`、`OR`
*   以及使用括号进行分组

## 循环语句

```cmake
foreach(<loop_var> <items>)
  <commands>
endforeach()
```

```cmake
set(LIST "a;b;c;d;e")
foreach(l ${LIST})
    MESSAGE(STATUS ${l})
endforeach()
```

    while(<condition>)
      <commands>
    endwhile()

<!---->

    set(count 0)
    while (count LESS 5)
        math(EXPR count "${count} + 1")
        message(STATUS ${count})
    endwhile()

## 生成器表达式

[generator expressions](https://cmake.org/cmake/help/latest/manual/cmake-generator-expressions.7.html)

`$<KEYWORD>`、`$<KEYWORD:value>`，`KEYWORD` 可以为 `1` 时 `value` 就会被保存下来，为 `0` 时为空

> \$<condition:true_string>，如果 condition 值为 1，则表达式被评估为 true\_string，否则为空值。

todo 例子

## 函数

使用 `function` 和 `endfunction` 标记函数，`ARGV` 中会存储所有变量，多个值会变成列表

```cmake
function(HELLO ARGV)
    MESSAGE(STATUS "hello, ${ARGV}!")
endfunction()

hello("cmake")
hello("c++", "c")
```

```txt
-- hello, cmake!
-- hello, c++;c!
```

### 函数参数

通过 `cmake_parse_arguments` 来解析函数参数

> cmake\_parse\_arguments(&lt;prefix&gt; &lt;options&gt; \<one\_value\_keywords> \<multi\_value\_keywords> &lt;args&gt;...)

```cmake
function(HELLO_2)
    cmake_parse_arguments(
        ARGN_PREFIX
        "FOO;FOO2"
        "BAR;BAR2"
        "LIST"
        ${ARGN}
    )
    MESSAGE(STATUS ${ARGN_PREFIX_FOO} ${ARGN_PREFIX_FOO2})
    MESSAGE(STATUS ${ARGN_PREFIX_BAR} ${ARGN_PREFIX_BAR2})
    MESSAGE(STATUS ${ARGN_PREFIX_LIST})
endfunction()

hello_2(FOO BAR "bar1" BAR2 "bar2" LIST "hello" "cmake" "!")
```

`FOO` 和 `FOO2` 是 `options` 参数，如果参数列表中出现了即为 `true`，如果未出现即为 `false`

## 调试 CMake

使用 `message` 输出值

    message(STATUS "MY_VARIABLE=${MY_VARIABLE}")

使用 `cmake_print_variables` 打印变量

```cmake
include(CMakePrintHelpers)
cmake_print_variables(MY_VARIABLE)
```

通过 `--trace-source` 输出文件运行的过程

```sh
cmake -S . -B build --trace-source=CMakeLists.txt
```

使用 `debug` 模式构建

# 选项、配置、标志和外部环境

## 选项

> option(&lt;variable&gt; "\<help\_text>" \[value])

```cmake
option(IS_HAHA "Haha or Wuuu?" TRUE)
if (${IS_HAHA})
    MESSAGE(STATUS "hahahahahahaha")
else()
    MESSAGE(STATUS "Wuuuuuuuuuuuuu")
endif()
```

```sh
cmake . -D IS_HAHA=FALSE
-- Wuuuuuuuuuuuuu
```

选项会被缓存到 `CMakeCache.txt`

```txt
// CMakeCache.txt
//Haha or Wuuu?
IS_HAHA:BOOL=FALSE
```

使用 `cmake_dependent_option` 可以让选项的值可以依赖于其他选项（首先要 `include(CMakeDependentOption)` 才能使用）

```cmake
include(CMakeDependentOption)

cmake_dependent_option(HAS_JOKE "has a joke" TRUE "IS_HAHA" FALSE)
if (${HAS_JOKE})
    MESSAGE(STATUS "has a joke")
endif()
```

## 指定编译器

编译器设定将存储在变量 `CMAKE_<LANG>_COMPILER` 中，可以用 `-D` 去设置

```sh
cmake -D CMAKE_CXX_COMPILER=clang++ ..
```

## 文件

### configure\_file

使用 `configure_file` 可以通过读取变量以及配置文件去生成所需的文件

```cpp
// foo.hpp.in
#define MSG "${MSG}"
```

```cmake
SET(MSG "lalalala hello")

configure_file(
    "foo.hpp.in"
    "foo.hpp"
)
```

最终会得到

```cpp
// foo.hpp
#define MSG "lalalala hello"
```

### file

`file` 命令有多种子命令实现不同的操作

[CMake file](https://cmake.org/cmake/help/latest/command/file.html)

> file(STRINGS &lt;filename&gt; &lt;variable&gt; \[&lt;options&gt;...])

通过 `STRINGS` 可以将文件读取成字符串赋值到变量中

## 运行外部程序

通过 `execute_process` 可以执行命令并且获取执行的结果。

下面是《Modern CMake》中更新子模块的例子，很好的体现了它的作用。

```cmake
find_package(Git QUIET)

if(GIT_FOUND AND EXISTS "${PROJECT_SOURCE_DIR}/.git")
    execute_process(COMMAND ${GIT_EXECUTABLE} submodule update --init --recursive
                    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
                    RESULT_VARIABLE GIT_SUBMOD_RESULT)
    if(NOT GIT_SUBMOD_RESULT EQUAL "0")
        message(FATAL_ERROR "git submodule update --init --recursive failed with ${GIT_SUBMOD_RESULT}, please checkout submodules")
    endif()
endif()
```

## 自定义命令

`add_custom_command`

`add_custom_target`

## 构建类型

```cmake
# Set a default build type if none was specified
set(default_build_type "Release")
if(EXISTS "${CMAKE_SOURCE_DIR}/.git")
  set(default_build_type "Debug")
endif()

if(NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
  message(STATUS "Setting build type to '${default_build_type}' as none was specified.")
  set(CMAKE_BUILD_TYPE "${default_build_type}" CACHE
      STRING "Choose the type of build." FORCE)
  # Set the possible values of build type for cmake-gui
  set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS
    "Debug" "Release" "MinSizeRel" "RelWithDebInfo")
endif()
```

几种类型的含义

*   Debug：用于在没有优化的情况下，使用带有调试符号构建库或可执行文件。
*   Release：用于构建的优化的库或可执行文件，不包含调试符号。
*   RelWithDebInfo：用于构建较少的优化库或可执行文件，包含调试符号。
*   MinSizeRel：用于不增加目标代码大小的优化方式，来构建库或可执行文件。

## 编译选项

打印所有标志

```cmake
message("C++ compiler flags: ${CMAKE_CXX_FLAGS}")
```

设置选项

> target\_compile\_options(&lt;target&gt; \[BEFORE] \<INTERFACE|PUBLIC|PRIVATE> \[items1...] \[\<INTERFACE|PUBLIC|PRIVATE> \[items2...] ...])

```cmake
target_compile_options(geometry PRIVATE ${flags})
```

编译选项有三种范围 `INTERFACE` `PUBLIC` `PRIVATE`

*   INTERFACE，应用于目标，并且传递给相关的目标
*   PUBLIC，应用于目标，并且会传递给目标的使用者
*   PRIVATE，只应用于目标

也可以通过 `-D` 直接设置 `CMAKE_CXX_FLAGS` 的方式设置选项，当然这样就不好进行细分了。

```sh
cmake -D CMAKE_CXX_FLAGS="..." .
```

## 目标属性

使用 `set_target_properties` 对目标的属性进行设置

> set\_target\_properties(target1 target2 ... PROPERTIES prop1 value1 prop2 value2 ...)

```cmake
add_executable(animal-farm animal-farm.cpp)
set_target_properties(animal-farm
  PROPERTIES
    CXX_STANDARD 14
    CXX_EXTENSIONS OFF
    CXX_STANDARD_REQUIRED ON
  )
```

*   CXX\_STANDARD C++ 标准的版本
*   CXX\_EXTENSIONS 是否只启用 IOS C++ 标准
*   CXX\_STANDARD\_REQUIRED 是否要求 C++ 标准的版本，设置 `OFF` 时如果版本不可用，会从高到底查找到能用的版本

使用 `target_compile_features` 可以更细致的控制目标的特性

## 操作系统类型

系统名称存储在变量 `CMAKE_SYSTEM_NAME` 中

```cmake
MESSAGE(STATUS ${CMAKE_SYSTEM_NAME})
```

根据操作系统可能的值为

*   `Linux`
*   `Darwin`
*   `Windows`
*   `AIX`

通过 `target_compile_definitions` 给目标在编译时设置 `define`

> target\_compile\_definitions(&lt;target&gt; \<INTERFACE|PUBLIC|PRIVATE> \[items1...] \[\<INTERFACE|PUBLIC|PRIVATE> \[items2...] ...])

```cmake
if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
  target_compile_definitions(foo PUBLIC "IS_LINUX")
endif()
```

```cpp
std::string say_hello() {
#ifdef IS_LINUX
  return std::string("Hello, Linux");
#elif
  ...
#endif
}
```

## 编译器类型

编译器类型存储在变量 `CMAKE_CXX_COMPILER_ID` 中

可能的值的具体定义 [CMAKE\_&lt;LANG&gt;\_COMPILER\_ID](https://cmake.org/cmake/help/latest/variable/CMAKE_LANG_COMPILER_ID.html)

```cmake
if(CMAKE_CXX_COMPILER_ID MATCHES GNU)
  target_compile_definitions(foo PUBLIC "IS_GNU_CXX_COMPILER")
endif()
```

## 处理器架构和指令集

通过 `CMAKE_SIZEOF_VOID_P` void pointer 的大小判断 64 位还是 32 位

```cmake
if(CMAKE_SIZEOF_VOID_P EQUAL 8)
  target_compile_definitions(foo PUBLIC "IS_64_BIT_ARCH")
else()
  target_compile_definitions(foo PUBLIC "IS_32_BIT_ARCH")
endif()
```

除了判断空指针的大小，不同平台也有表明的处理器名称的变量

*   Linux 在 `CMAKE_HOST_SYSTEM_PROCESSOR` 中
*   Windows 在 `PROCESSOR_ARCHITECTURE` 中
*   macOS Apple Silicon 处理器的在变量 `CMAKE_APPLE_SILICON_PROCESSOR` 中），其他的在 `CMAKE_OSX_ARCHITECTURES` 中

使用 `cmake_host_system_information` 查询更多平台的详细信息

```cmake
foreach(key
  IN ITEMS
    NUMBER_OF_LOGICAL_CORES
    NUMBER_OF_PHYSICAL_CORES
    TOTAL_VIRTUAL_MEMORY
    AVAILABLE_VIRTUAL_MEMORY
    TOTAL_PHYSICAL_MEMORY
    AVAILABLE_PHYSICAL_MEMORY
    IS_64BIT
    HAS_FPU
    HAS_MMX
    HAS_MMX_PLUS
    HAS_SSE
    HAS_SSE2
    HAS_SSE_FP
    HAS_SSE_MMX
    HAS_AMD_3DNOW
    HAS_AMD_3DNOW_PLUS
    HAS_IA64
    OS_NAME
    OS_RELEASE
    OS_VERSION
    OS_PLATFORM
  )
  cmake_host_system_information(RESULT _${key} QUERY ${key})
  MESSAGE(STATUS "${key}: ${_${key}}")
endforeach()
```

# Git

## git 子模块

```cmake
find_package(Git QUIET)
if(GIT_FOUND AND EXISTS "${PROJECT_SOURCE_DIR}/.git")
# Update submodules as needed
    option(GIT_SUBMODULE "Check submodules during build" ON)
    if(GIT_SUBMODULE)
        message(STATUS "Submodule update")
        execute_process(COMMAND ${GIT_EXECUTABLE} submodule update --init --recursive
                        WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
                        RESULT_VARIABLE GIT_SUBMOD_RESULT)
        if(NOT GIT_SUBMOD_RESULT EQUAL "0")
            message(FATAL_ERROR "git submodule update --init --recursive failed with ${GIT_SUBMOD_RESULT}, please checkout submodules")
        endif()
    endif()
endif()

if(NOT EXISTS "${PROJECT_SOURCE_DIR}/extern/repo/CMakeLists.txt")
    message(FATAL_ERROR "The submodules were not downloaded! GIT_SUBMODULE was turned off or failed. Please update submodules and try again.")
endif()
```

## 获取 git commit id

```cmake
execute_process(COMMAND ${GIT_EXECUTABLE} rev-parse --short HEAD
                WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
                OUTPUT_VARIABLE PACKAGE_GIT_VERSION
                ERROR_QUIET
                OUTPUT_STRIP_TRAILING_WHITESPACE)
```

## 从 git 获取

> FetchContent\_Declare(&lt;name&gt; &lt;contentOptions&gt;... \[EXCLUDE\_FROM\_ALL] \[SYSTEM] \[OVERRIDE\_FIND\_PACKAGE | FIND\_PACKAGE\_ARGS args...])

```cmake
FetchContent_Declare(
  googletest
  GIT_REPOSITORY https://github.com/google/googletest.git
  GIT_TAG        703bd9caab50b139428cea1aaff9974ebee5742e # release-1.10.0
)
FetchContent_Declare(
  myCompanyIcons
  URL      https://intranet.mycompany.com/assets/iconset_1.12.tar.gz
  URL_HASH MD5=5588a7b18261c20068beabfb4f530b87
)

FetchContent_MakeAvailable(googletest myCompanyIcons)
```
