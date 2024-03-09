set(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)

add_executable(use_hello.x use_hello.cc)

find_package(hello_shared)

target_link_libraries(use_hello.x PRIVATE hello_shared::hello_shared)

#set_property(TARGET use_hello.x PROPERTY INSTALL_RPATH_USE_LINK_PATH TRUE)

install(TARGETS use_hello.x DESTINATION "${PROJECT_SOURCE_DIR}/run")
