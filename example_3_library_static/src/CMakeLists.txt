
add_library(hello STATIC)

target_sources(hello
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
    TARGETS hello                                       # install library
    EXPORT  hello_exp                                   # define export var for next comand
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    FILE_SET hello_headers DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)

install(
    EXPORT hello_exp                                    # hello export file
    FILE hello_exp.cmake
    NAMESPACE hello::
    DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/hello"
)

install(
    FILES "helloConfig.cmake"                           # install config files
    DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/hello"   # edit file helloConfig.cmake
)
