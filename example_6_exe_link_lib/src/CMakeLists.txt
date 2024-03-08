
add_executable(use_hello.x)
target_sources(use_hello.x PRIVATE use_hello.cc)

find_package(hello_shared)
target_link_libraries(use_hello.x PRIVATE hello_shared::hello_shared)

if(APPLE)
    set_property(TARGET use_hello.x PROPERTY INSTALL_RPATH_USE_LINK_PATH TRUE)  # adds LC_RPATH to executable
endif()

install(TARGETS use_hello.x DESTINATION "${PROJECT_SOURCE_DIR}/run")
