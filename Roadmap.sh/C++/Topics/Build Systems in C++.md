A build system is a collection of tools and utilities that automate the process of compiling, linking, and executing source code files in a project. The primary goal of build systems is to manage the complexity of the compilation process and produce a build in the end.

#### CMake
```
cmake_minimum_required(VERSION 3.0)

project(MyProject)

set(SRC_DIR "${CMAKE_CURRENT_LIST_DIR}/src")
set(SOURCES "${SRC_DIR}/main.cpp" "${SRC_DIR}/file1.cpp" "${SRC_DIR}/file2.cpp")

add_executable(${PROJECT_NAME} ${SOURCES})

target_include_directories(${PROJECT_NAME} PRIVATE "${CMAKE_CURRENT_LIST_DIR}/include")

set_target_properties(${PROJECT_NAME} PROPERTIES
    CXX_STANDARD 14
    CXX_STANDARD_REQUIRED ON
    CXX_EXTENSIONS OFF
)
```

### Package Managers
Some popular package managers used in the C++ ecosystem include:
	- Conan
	- vcpkg
	- C++ Archive Network (cppan)

### Working with Libraries in C++
In C++ libraries can be either static libraries (.lib) or dynamic libraries (.dll).

#### 1.) Static Libraries
Static libraries are incorporated into your program during compile time. They are linked with your code, creating a larger executable file, but it does not require any external files during runtime. 

#### 2.) Dynamic Libraries
Dynamic libraries are loaded during runtime, which means that your executable file only contains references to these libraries. The libraries need to be available on the system where your program is running.