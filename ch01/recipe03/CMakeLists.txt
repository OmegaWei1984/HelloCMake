cmake_minimum_required(VERSION 3.5 FATAL_ERROR)
project(recipe03 LANGUAGES CXX)
add_executable(hello main.cpp)
add_library(message
  STATIC
    Message.hpp
    Message.cpp
  )
target_link_libraries(hello message)
