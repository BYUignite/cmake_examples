set(CMAKE_INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/lib")     # for exe to find local lib
set(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)                # for exe to find external lib

add_executable(use_libs.x use_libs.cc)

find_library(BEATIT beatit_shared)
find_path(BEATIT_INC beatit.h)

target_include_directories(use_libs.x PRIVATE "${PROJECT_SOURCE_DIR}/src_lib")
target_include_directories(use_libs.x PRIVATE "${BEATIT_INC}")
target_link_libraries(use_libs.x PRIVATE hello_shared9 ${BEATIT}) # local hello_shared and external BEATIT

install(TARGETS use_libs.x DESTINATION "${PROJECT_SOURCE_DIR}/run")
