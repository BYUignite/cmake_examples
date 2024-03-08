cmake_minimum_required(VERSION 3.28)

project(example LANGUAGES CXX)

######################################

set(CMAKE_VERBOSE_MAKEFILE ON)
set(CMAKE_CXX_STANDARD 20)

######################################

add_subdirectory(src)
