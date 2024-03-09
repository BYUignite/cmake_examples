
add_library(hello_shared9 SHARED)

target_sources(hello_shared9
    PRIVATE
        hello.cc
    PUBLIC    
        FILE_SET hello_headers
            TYPE HEADERS
            BASE_DIRS "${CMAKE_CURRENT_SOURCE_DIR}"
            FILES hello.h
)

#-------------------------------------
# install: library, and config files for use with find_package in some other lib/exe

include(GNUInstallDirs)

install(
    TARGETS hello_shared9                                # install library
    EXPORT  hello_shared9_exp                            # define export var for next comand
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    FILE_SET hello_headers DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)

install(
    EXPORT hello_shared9_exp                             # hello export file
    FILE hello_shared9_exp.cmake
    NAMESPACE hello_shared9::
    DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/hello_shared9"
)

install(
    FILES "hello_shared9Config.cmake"                           # install config files
    DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/hello_shared9"   # edit file hello_shared9Config.cmake
)
