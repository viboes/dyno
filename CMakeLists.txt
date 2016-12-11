# Copyright Louis Dionne 2016
# Distributed under the Boost Software License, Version 1.0.
# (See accompanying file LICENSE.md or copy at http://boost.org/LICENSE_1_0.txt)

cmake_minimum_required(VERSION 3.7)
project(TE VERSION 0.0.1 LANGUAGES CXX)
# TODO: Set these as interface properties when supported
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED YES)


# Setup Hana, which is a dependency
add_library(hana INTERFACE)
target_include_directories(hana INTERFACE ~/code/hana/include)


# Setup the `te` library target
add_library(te INTERFACE)
target_include_directories(te INTERFACE include)
target_link_libraries(te INTERFACE hana)


# Setup the `check` target to build and then run all the tests and examples.
add_custom_target(check
  COMMAND ${CMAKE_CTEST_COMMAND} --output-on-failure
  WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
  COMMENT "Build and run all the tests and examples.")


# Setup subdirectories
enable_testing()
add_subdirectory(example)