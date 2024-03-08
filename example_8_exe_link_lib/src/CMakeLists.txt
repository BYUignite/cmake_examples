
add_executable(use_beatit.x)
target_sources(use_beatit.x PRIVATE use_beatit.cc)

find_library(BEATIT beatit)
find_path(BEATIT_INC beatit.h)

target_include_directories(use_beatit.x PRIVATE "${BEATIT_INC}")
target_link_libraries(use_beatit.x PRIVATE ${BEATIT})

install(TARGETS use_beatit.x DESTINATION "${PROJECT_SOURCE_DIR}/run")
