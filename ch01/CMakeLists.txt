cmake_minimum_required(VERSION 3.5 FATAL_ERROR)
project(ch01 LANGUAGES CXX)

set(USE_LIBRARY ON)
message(STATUS "Compile sources into a library? ${USE_LIBRARY}")

# # add_library will create a static library
# set(BUILD_SHARED_LIBS OFF)

list(APPEND _sources Message.hpp Message.cpp)

set(IS_STATIC 1)
message(STATUS "Compile sources into a static library? ${IS_STATIC}")
if(IS_STATIC)
    set(TYPE STATIC)
else()
    set(TYPE SHARED)
endif()

set(IS_OBJECT Y)
message(STATUS "Compile sources into a object library? ${IS_OBJECT}")
if(IS_OBJECT)
    set(TYPE OBJECT)
endif()

if(USE_LIBRARY)
    add_library(message ${TYPE} ${_sources})
    message(STATUS ${TYPE})
    add_executable(hello main.cpp)
    target_link_libraries(hello message)
else()
    add_executable(hello main.cpp ${_sources})
endif()
