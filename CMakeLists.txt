#
# Copyright (c) 2016-2017 Kris Jusiak (kris at jusiak dot net)
#
# Distributed under the Boost Software License, Version 1.0.
# (See accompanying file LICENSE_1_0.txt or copy at
# http://www.boost.org/LICENSE_1_0.txt)
#
cmake_minimum_required(VERSION 2.8)
project(GUnit CXX)

set(MASTER_PROJECT OFF)
if(CMAKE_CURRENT_SOURCE_DIR STREQUAL CMAKE_SOURCE_DIR)
  set(MASTER_PROJECT ON)
endif()

option(GUNIT_ENABLE_MEMCHECK "Run the unit tests and examples under valgrind if it is found." OFF)
option(GUNIT_ENABLE_COVERAGE "Run coverage." OFF)
option(GUNIT_BUILD_BENCHMARKS "Build the benchmarks" ${MASTER_PROJECT})
option(GUNIT_BUILD_EXAMPLES "Build the examples" ${MASTER_PROJECT})
option(GUNIT_BUILD_TESTS "Build the tests" ${MASTER_PROJECT})

add_custom_target(style)
add_custom_command(TARGET style COMMAND find ${CMAKE_CURRENT_LIST_DIR}/benchmark ${CMAKE_CURRENT_LIST_DIR}/example ${CMAKE_CURRENT_LIST_DIR}/include ${CMAKE_CURRENT_LIST_DIR}/test -iname "*.h" -or -iname "*.cpp" | xargs clang-format -i)

set(CMAKE_CXX_STANDARD 14)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wextra")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Werror")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pedantic")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pedantic-errors")

if(ENABLE_COVERAGE)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} --coverage")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g -O0")
endif()

# enable_testing()

# add_subdirectory(libs/googletest)
link_directories()

add_library(gunit INTERFACE)
target_include_directories(gunit INTERFACE include)
target_include_directories(gunit
  INTERFACE ./thrid-party/install/include)
#target_include_directories(gunit
#  INTERFACE ${gtest_SOURCE_DIR}/include
#  ${gmock_SOURCE_DIR}/include
#  libs/json/single_include/nlohmann
#)

target_link_directories(gunit INTERFACE ./thrid-party/install/lib)
#target_link_libraries(gunit
#  INTERFACE gtest_main
#  INTERFACE gmock_main
#  INTERFACE gherkin-cpp
#)

#set(BUILD_GMOCK)
#set(BUILD_GTEST)

#add_subdirectory(libs/gherkin-cpp)
