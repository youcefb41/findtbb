## Introduction ##

This web page contains information about an unofficial version of the FindTBB.cmake script I developed for my own TBB programs.

For more information about CMake and TBB:

  * http://www.cmake.org
  * http://threadingbuildingblocks.org/

The script eliminates the need to set visual studio build options manually.

The script is used and tested on WinXP. If you use another OS (Vista, Linux, Mac, Sun), please give it a try and contact me for support.

This webpage is updated infrequently - the svn log contains details about bug fixes and updates.

Please send any comments or questions to my email or the [issue tracker](http://code.google.com/p/findtbb/issues/list).

[Hannes Hofmann](http://www5.informatik.uni-erlangen.de/our-team/hofmann-hannes/),<br />
[Pattern Recognition Lab (Lehrstuhl fuer Muestererkennung, LME)](http://www5.informatik.uni-erlangen.de/), University of Erlangen-Nürnberg, Germany


## Obtaining FindTBB.cmake ##

The code is available in an svn repository: http://findtbb.googlecode.com/svn/trunk

Either checkout the example project:

```
svn co http://findtbb.googlecode.com/svn/trunk FindTBB
```

Or link the FindTBB.cmake and related files to an existing repository:

```
cd my_repository/CMake
svn propset svn:externals "FindTBB http://findtbb.googlecode.com/svn/trunk/CMake/modules" .
```


## Usage ##

After installing TBB add the install path in the corresponding tbbvars[.bat|.csh|.sh] and execute this script in your OS startup. FindTBB will use the environment variables `TBB30_INSTALL_DIR` (or `TBB22_INSTALL_DIR` for TBB 2.2, or `TBB21_INSTALL_DIR` for 2.1, or `TBB_INSTALL_DIR` as fallback) and `TBB_ARCH_PLATFORM` to find the include and lib directories.

For backwards compatibility, the CMake variables `TBB_ARCHITECTURE` and `TBB_COMPILER` are supported as well. This may change in a future release.

The script defines the following CMake variables:

| `TBB_FOUND` | Is TBB installed and found. |
|:------------|:----------------------------|
| `TBB_INCLUDE_DIRS` | TBB library headers.        |
| `TBB_LIBRARY_DIRS` | TBB library directory.      |
| `TBB_LIBRARIES` | TBB libraries (tbb, tbbmalloc). |
| `TBB_DEBUG_LIBRARIES` | TBB libraries with debug symbols (tbb\_debug, tbbmalloc\_debug). |

The following examples show how to include the script in your `CMakeLists.txt` file.

```
# Add FindTBB directory to CMake's module path
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/../CMake/FindTBB/")

# Execute the FindTBB macro
find_package(TBB)
# If you want FindTBB to fail if TBB is not found, use this form:
# find_package(TBB REQUIRED)

if(NOT TBB_FOUND)
        MESSAGE (STATUS "TBB not found. Example project will not be built.")
else(NOT TBB_FOUND)

# Here goes the actual project
include_directories(${TBB_INCLUDE_DIRS})
link_directories(${TBB_LIBRARY_DIRS})
add_executable(FindTBB_example ${FindTBB_example_SRCS_CPP})

endif(NOT TBB_FOUND)
```


### Linux ###

FindTBB.cmake was developed under Windows but should work under Linux as well.

If it does not work for you, [Comments and suggestions](#Contact.md) to make FindTBB work more smoothly on Linux are appreciated.


## Building the Example Project ##

Below is an example of the commands needed to build the example project on Windows. On linux the process is roughly the same except that command line tools have to be used.

  1. Use TortoiseSVN to check out FindTBB.cmake from http://findtbb.googlecode.com/svn/trunk/ to D:\FindTBB-test\svn\
  1. Copy the file `sub_string_finder.cpp` from Intel's TBB examples to D:\FindTBB-test\svn\src\
  1. Open cmake-gui (currently beta) and use D:\FindTBB-test\svn\ and D:\FindTBB-test\build\ as source and build directories respectively
  1. Press 'Configure', select your VS version and wait
  1. Press 'Configure' again
  1. Press 'Generate'
  1. Go to D:\FindTBB-test\build\ and open FindTBB\_pkg.sln


## License ##

This script is released under the MIT license.


## Contact ##

I don't like to publish my email address here, but you can find it (and further contact information) on my [website](http://www5.informatik.uni-erlangen.de/our-team/hofmann-hannes/). You can also use the [issue tracker](http://code.google.com/p/findtbb/issues/list).


## Thanks ##

... to Florian Uhlig, for the TBB 2.2 and 3.0 patch<br />
... to Gino van den Bergen for the `TBB_ARCH_PLATFORM` patch<br />
... to [Abe Stephens](http://www.sci.utah.edu/~abe/) for his [FindCuda](http://www.sci.utah.edu/~abe/FindCuda.html) homepage which was very inspiring.