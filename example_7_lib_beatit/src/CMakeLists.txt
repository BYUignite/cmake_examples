
add_library(beatit STATIC)

target_sources(beatit
    PRIVATE
        beatit.cc
    PUBLIC    
        FILE_SET beatit_headers
            TYPE HEADERS
            BASE_DIRS "${CMAKE_CURRENT_SOURCE_DIR}"
            FILES beatit.h
)

#-------------------------------------
# install: library, and config files for use with find_package in some other lib/exe

include(GNUInstallDirs)

install(
    TARGETS beatit
    FILE_SET beatit_headers DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)

####################################################

add_library(beatit_shared SHARED)

target_sources(beatit_shared
    PRIVATE
        beatit.cc
    PUBLIC    
        FILE_SET beatit_headers
            TYPE HEADERS
            BASE_DIRS "${CMAKE_CURRENT_SOURCE_DIR}"
            FILES beatit.h
)

#-------------------------------------
# install: library, and config files for use with find_package in some other lib/exe

include(GNUInstallDirs)

install(
    TARGETS beatit_shared
    FILE_SET beatit_headers DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)
