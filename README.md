### Examples of using modern CMake
* These are setup and run on Mac with Sonoma 14.3.1 on an Apple M3 Pro 2023
* The examples include building an executable, a library, and linking against a library
    * Static and shared libraries are demonstrated
    * The libraries include installation with a config file for use in downstream packages with ```find_package```, and also in linking against libraries and headers without cmake information.
* Efforts have been made to use modern CMake features, but corrections or suggestions are appreciated.
    * Note that there are usually multiple approaches, and multiple commands and options, not all of which are needed. 
    * These examples are meant to be simple and minimal, and useful for nonexperts that need a place to start with some of the essential features.
* In all cases the usual build process can be applied:
```
mkdir build
cd build
cmake ..
make
make install
```

For examples that use installed libraries, tell CMake where to look for them by setting evironment variable ```CMAKE_PREFIX_PATH```: 
```
export CMAKE_PREFIX_PATH="$CMAKE_PREFIX_PATH:/path/to/cmake_examples/usr/example_3"
export CMAKE_PREFIX_PATH="$CMAKE_PREFIX_PATH:/path/to/cmake_examples/usr/example_4"
export CMAKE_PREFIX_PATH="$CMAKE_PREFIX_PATH:/path/to/cmake_examples/usr/example_7"
```

#### Example 1
* Build a simple top level executable that prints "hi there" to the screen.
* Includes a class ```hello``` (that prints) and a main that drives.

#### Example 2
* Redo example 1, but with a directory structure.
    * source code in ```src```
    * installed executable in ```run```

#### Example 3
* Redo examples 1 and 2, but install the ```hello``` class as a static library.
* Installed in ```./usr/example_3```

#### Example 4
* Same as example 3 but a shared library instead of static
* Installed in ```./usr/example_4```

#### Example 5
* Build an executable that links against the static library in example 3.

#### Example 6
* Same as example 5, but link against the shared library in example 4.
* See notes for example 9 for use of the command ```set(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)```

#### Example 7
* Install a simple library ```beatit``` that is used by example 8
* Installed without a corresponding config file for use with find_package.
* Installed in ```./usr/example_7```
* Both static and shared installed

#### Example 8
* Build an executable that links against the static library in example 7.
* Demonstrates including libraries (example 8) without a package.
    * Uses ```find_library```, and ```find_path``` instead of ```find_package```
* **Note**, ```target_link_directories``` is not needed when using ```find_library(BEATIT beatit)``` followed by ```target_link_libraries(use_beatit.x PRIVATE ${BEATIT})```
    * It would be needed if we did ```target_link_libraries(use_beatit.x PRIVATE beatit)``` instead to directly link to the library.

#### Example 9
* Combine examples 4 and 6, that is, build the library and executable in one project.
* Also link against an external library, beatit, from Example 7.
* This is done with shared libraries and demonstrates the need for RPATH handling.
    * In particular ```set(CMAKE_INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/lib")``` is needed for the internal (to the project) library, and ```set(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)``` is needed for the the external library.
    * See [RPATH Handling](https://gitlab.kitware.com/cmake/community/-/wikis/doc/cmake/RPATH-handling) for a very detailed and clear description, especially the paragraph halfway down starting with ```CMAKE_INSTALL_RPATH_USE_LINK_PATH```.
        * In short, the RPATH treatment is different for build and install steps. By default, build will have RPATH for the local and external libraries, but the install will have neither. The first command above will include the local library in the RPATH (because we are explicitly adding it). The second will include any linked RPATHS except those in the build tree (that is, the local library).
* Use ```otool -l use_libs.x``` to see the ```@rpath``` as well as the ```LC_RPATH``` that resolves the location.


