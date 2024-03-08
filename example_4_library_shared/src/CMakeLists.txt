
add_library(hello_shared SHARED)

target_sources(hello_shared
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
    TARGETS hello_shared                                # install library
    EXPORT  hello_shared_exp                            # define export var for next comand
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    FILE_SET hello_headers DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)

install(
    EXPORT hello_shared_exp                             # hello export file
    FILE hello_shared_exp.cmake
    NAMESPACE hello_shared::
    DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/hello_shared"
)

install(
    FILES "hello_sharedConfig.cmake"                           # install config files
    DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/hello_shared"   # edit file hello_sharedConfig.cmake
)
