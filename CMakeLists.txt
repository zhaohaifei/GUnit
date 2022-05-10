#
# Copyright (c) 2016-2017 Kris Jusiak (kris at jusiak dot net)
#
# Distributed under the Boost Software License, Version 1.0.
# (See accompanying file LICENSE_1_0.txt or copy at
# http://www.boost.org/LICENSE_1_0.txt)
#
cmake_minimum_required(VERSION 3.9.0)
project("GUnit" C CXX)

add_custom_target(style)
add_custom_command(TARGET style COMMAND find ${CMAKE_CURRENT_LIST_DIR}/benchmark ${CMAKE_CURRENT_LIST_DIR}/example ${CMAKE_CURRENT_LIST_DIR}/include ${CMAKE_CURRENT_LIST_DIR}/test -iname "*.h" -or -iname "*.cpp" | xargs clang-format -i)

#set(CMAKE_CXX_STANDARD 11)

# add_library(gunit OBJECT include)
# target_include_directories(gunit PUBLIC include)
# target_include_directories(gunit PUBLIC ./thrid-party/install/include)
# target_link_directories(gunit PUBLIC ./thrid-party/install/lib)

add_executable(GTest GTest.cpp)
include_directories(AFTER ${CMAKE_SOURCE_DIR}/include)
include_directories(AFTER ${CMAKE_SOURCE_DIR}/thrid-party/install/include)

link_directories(AFTER ${CMAKE_SOURCE_DIR}/thrid-party/install/lib)

