
add_executable(use_hello.x)
target_sources(use_hello.x PRIVATE use_hello.cc hello.cc)

install(TARGETS use_hello.x DESTINATION "${PROJECT_SOURCE_DIR}/run")
