# CMake Cookbook

按照 [CMake菜谱（CMake Cookbook中文版）](https://www.bookstack.cn/read/CMake-Cookbook/README.md)一步步学习 CMake

## 实验环境
```sh
# 使用 docker 镜像
docker run -v $my_repo:/home/mightybuilder/CMakeCookbook -it devcafe/cmake-cookbook_ubuntu-18.04
```

## 笔记

### ch01

将单个源文件编译为可执行文件；
```sh
mkdir build
cd build
cmake ..
# 或者直接
cmake -H. -Bbuild
```
`-H` 指定了查找 CMakeLists.txt 的目录，`-B` 指定了生成目录。
