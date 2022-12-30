cmake_minimum_required(VERSION 3.5 FATAL_ERROR)
project(recipe03 LANGUAGES CXX)
add_executable(hello main.cpp)
## static
# add_library(message
#   STATIC
#     Message.hpp
#     Message.cpp
#   )
# target_link_libraries(hello message)

## object
add_library(message-objs
  OBJECT
      Message.hpp
      Message.cpp
  )
add_library(message-shared
  SHARED
      $<TARGET_OBJECTS:message-objs>
  )
add_library(message-static
  STATIC
      $<TARGET_OBJECTS:message-objs>
  )
target_link_libraries(hello message-static)
