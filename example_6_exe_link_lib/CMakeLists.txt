cmake_minimum_required(VERSION 3.23)

project(myproject LANGUAGES CXX)

######################################

set(CMAKE_VERBOSE_MAKEFILE ON)
set(CMAKE_CXX_STANDARD 20)

######################################

add_subdirectory(src)
