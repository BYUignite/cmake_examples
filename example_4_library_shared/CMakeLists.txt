cmake_minimum_required(VERSION 3.28)

project(myproject LANGUAGES CXX)

######################################

set(CMAKE_VERBOSE_MAKEFILE ON)
set(CMAKE_CXX_STANDARD 20)

set(CMAKE_INSTALL_PREFIX "${CMAKE_SOURCE_DIR}/../usr/example_4")

######################################

add_subdirectory(src)
