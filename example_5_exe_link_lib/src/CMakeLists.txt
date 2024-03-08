
add_executable(use_hello.x)
target_sources(use_hello.x PRIVATE use_hello.cc)

find_package(hello)
target_link_libraries(use_hello.x PRIVATE hello::hello)

install(TARGETS use_hello.x DESTINATION "${PROJECT_SOURCE_DIR}/run")
