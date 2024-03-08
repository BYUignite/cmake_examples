cmake_minimum_required(VERSION 3.28)

project(example LANGUAGES CXX)

######################################

set(CMAKE_VERBOSE_MAKEFILE ON)
set(CMAKE_CXX_STANDARD 20)

######################################

add_executable(use_hello.x)
target_sources(use_hello.x PRIVATE use_hello.cc hello.cc)

install(TARGETS use_hello.x DESTINATION "${PROJECT_SOURCE_DIR}")
