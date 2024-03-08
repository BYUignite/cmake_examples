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
* **Note**, set an environment variable ```set CMAKE_PREFIX_PATH=/path/to/installed/example_3``` so that the find_package(hello) command finds the installed hello library.

#### Example 6
* Same as example 5, but link against the shared library in example 4.
* **Note**, set an environment variable ```set CMAKE_PREFIX_PATH=/path/to/installed/example_4``` so that the ```find_package(hello_shared)``` command finds the installed ```hello_shared``` library.

#### Example 7
* Install a simple library ```beatit``` that is used by example 8
* Installed without a corresponding config file for use with find_package.
* Installed in ```./usr/example_7```

#### Example 8
* Build an executable that links against the library in example 7.
* Demonstrates including libraries (example 8) without a package.
    * Uses ```find_library```, and ```find_path``` instead of ```find_package```
* **Note**, set an environment variable ```set CMAKE_PREFIX_PATH=/path/to/installed/example_7``` so that the ```find_library(beatit)``` command finds the installed ```beatit``` library.
* **Note**, ```target_link_directories``` is not needed when using ```find_library(BEATIT beatit)``` followed by ```target_link_libraries(use_beatit.x PRIVATE ${BEATIT})```
    * It would be needed if we did ```target_link_libraries(use_beatit.x PRIVATE beatit)``` instead to directly link to the library.
