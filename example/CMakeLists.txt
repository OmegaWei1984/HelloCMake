cmake_minimum_required(VERSION 3.12...3.20)
project(
    example VERSION 1.0
    DESCRIPTION "example"
    LANGUAGES CXX)

MESSAGE(STATUS "${VAR1}! CMake")
set(VAR1 "hello")
MESSAGE(STATUS "${VAR1}! CMake")

set(CACHE_VAR "lalala" CACHE STRING "Comment")
MESSAGE(STATUS "cache var ${CACHE_VAR}")

set(foo "bar")
set(bar "hello")
MESSAGE(STATUS "I am ${foo}")
MESSAGE(STATUS "${${foo}}")

function(HELLO ARGV)
    MESSAGE(STATUS "hello, ${ARGV}!")
endfunction()

hello("cmake")
hello("c++" "c")

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

option(IS_HAHA "Haha or Wuuu?" TRUE)
if (${IS_HAHA})
    MESSAGE(STATUS "hahahahahahaha")
else()
    MESSAGE(STATUS "Wuuuuuuuuuuuuu")
endif()

include(CMakeDependentOption)

cmake_dependent_option(HAS_JOKE "has a joke" TRUE "IS_HAHA" FALSE)
if (${HAS_JOKE})
    MESSAGE(STATUS "has a joke")
endif()

SET(MSG "lalalala hello")

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

if(USE_LIBRARY)
    if (IS_OBJECT)
        add_library(message-objs OBJECT Message.hpp Message.cpp)

        add_library(message-shared SHARED $<TARGET_OBJECTS:message-objs> )
        set_target_properties(message-shared PROPERTIES OUTPUT_NAME "message")

        add_library(message-static STATIC $<TARGET_OBJECTS:message-objs>)
        set_target_properties(message-static PROPERTIES OUTPUT_NAME "message")

        add_executable(hello main.cpp)

        target_link_libraries(hello message-static)
    else()
        add_library(message ${TYPE} ${_sources})
        message(STATUS ${TYPE})
        add_executable(hello main.cpp)
        target_link_libraries(hello message)
    endif()
    
else()
    add_executable(hello main.cpp ${_sources})
endif()
