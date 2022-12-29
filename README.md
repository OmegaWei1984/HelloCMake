# CMake Cookbook

按照 [CMake菜谱（CMake Cookbook中文版）](https://www.bookstack.cn/read/CMake-Cookbook/README.md)一步步学习 CMake

## 实验环境
```sh
# 使用 docker 镜像
docker run -v $my_repo:/home/mightybuilder/CMakeCookbook -it devcafe/cmake-cookbook_ubuntu-18.04
```

## 笔记

### ch01

#### 1.1 将单个源文件编译为可执行文件
```sh
mkdir build
cd build
cmake ..
# 或者直接
cmake -H. -Bbuild
make .
```
`-H` 指定了查找 CMakeLists.txt 的目录，`-B` 指定了生成目录。
CMake 默认生成 Unix Makefile，然后通过 `make` 命令根据其来构建项目。 

#### 1.2 切换生成器

使用 `-G` 指定 Generator；
```sh
# 先清理 build 下的文件
# Either remove the CMakeCache.txt file and CMakeFiles directory or choose a different binary directory.
cmake -G Ninja ..
cmake --build .
```
build.ninja 和 rules.ninja 为 Ninja 的生成的构建语句和构建规则，然后通过 `cmake --build` 根据上述文件来构建项目。

    cmake --build . 将 ninja 命令封装在一个跨平台的接口中。
