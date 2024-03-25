# CMake

## General Info

### 1. CMake Command Line

CMake is a widely-used tool for managing the build process of software projects. It uses a text-based configuration file called CMakeLists.txt to generate build files for various platforms and build systems such as Makefiles, Visual Studio projects, and Xcode projects.

The basic command-line usage of CMake typically involves running the `cmake` command followed by options and arguments. Here's a basic overview of common CMake command-line options:

1. **cmake [<path-to-source>]**:
   - This command initializes the build system in the current directory (if `<path-to-source>` is not specified) or in the specified directory.

2. **-G "<generator>"** or **--generator="<generator>"**:
   - Specifies the build system generator to be used. For example, "Unix Makefiles" for Makefiles on Unix-like systems, "Visual Studio 16 2019" for Visual Studio projects.

3. **-DCMAKE_VARIABLE=value**:
   - Allows you to set CMake variables directly from the command line. These variables can influence the configuration of the build process. For example, `-DCMAKE_BUILD_TYPE=Release` sets the build type to Release.

4. **-S <path-to-source> -B <path-to-build>**:
   - Specifies separate source and build directories, which can be useful for out-of-source builds.

5. **--build <path-to-build> [--target <target>] [--config <config>]**:
   - Invokes the underlying build system to build the project. You can specify a particular target to build with `--target`, and a configuration (e.g., Debug, Release) with `--config`.

6. **--install <path-to-build>**:
   - Installs the built targets, headers, and other resources to the specified installation prefix.

7. **--build <path-to-build> --target install**:
   - This is a common combination to build and install the project in one step.

8. **--clean-first**:
   - Cleans the build directory before building. Useful for ensuring a clean build.

9. **--help**:
   - Displays help information about CMake command-line options.

These are some of the most commonly used options, but there are many more available. You can always refer to the official CMake documentation for more detailed information and advanced options.

### 1. Basic Project Strcuture

Creating a basic project structure using CMake involves several steps. CMake is a cross-platform tool that helps in managing the build process of software projects. Here's a simple example of how you can structure a project using CMake:

1. **Create Project Directory**: Start by creating a directory for your project. This will serve as the root directory for your project.

```plaintext
MyProject/
```

1. **Create Source Files**: Inside your project directory, create the necessary source files for your project. For this example, let's assume you have a simple C++ project with two source files.

```plaintext
MyProject/
    |-- src/
        |-- main.cpp
        |-- utils.cpp
    |-- CMakeLists.txt
```

1. **Write Source Code**: Write your source code files (`main.cpp` and `utils.cpp`). For this example, let's create some simple code.

`main.cpp`:

```cpp
#include <iostream>
#include "utils.h"

int main() {
    std::cout << "Hello, CMake!" << std::endl;
    std::cout << "Adding 5 and 3: " << add(5, 3) << std::endl;
    return 0;
}
```

`utils.cpp`:

```cpp
int add(int a, int b) {
    return a + b;
}
```

`utils.h`:

```cpp
#ifndef UTILS_H
#define UTILS_H

int add(int a, int b);

#endif
```

1. **Write CMakeLists.txt**: Now, create a `CMakeLists.txt` file in your project directory to specify how your project should be built.

```cmake
# CMakeLists.txt

cmake_minimum_required(VERSION 3.10)
project(MyProject)

# Locate source files
file(GLOB SOURCE_FILES "src/*.cpp")

# Add executable target
add_executable(MyProject ${SOURCE_FILES})
```

1. **Build the Project**: Navigate to your project directory in a terminal or command prompt and execute the following commands to build your project using CMake:

```bash
mkdir build
cd build
cmake ..
make
```

This will generate the necessary build files and compile your project. After building, you can find the executable `MyProject` in the `build` directory.

That's it! You've now created a basic project structure using CMake. This structure can be expanded upon as your project grows, and CMake provides a flexible way to manage increasingly complex build processes.

### 1. Intermediate Project Structure

Creating an intermediate project structure using CMake involves organizing your project into multiple directories, each containing its own set of source files, headers, and potentially subprojects. Here's a basic example of how you might structure your project and write the corresponding CMakeLists.txt files:

```bash
project/
│
├── CMakeLists.txt
│
├── src/
│   ├── CMakeLists.txt
│   ├── main.cpp
│   └── ...
│
├── include/
│   └── project_name/
│       ├── header1.hpp
│       └── ...
│
└── lib/
    ├── CMakeLists.txt
    ├── library1/
    │   ├── CMakeLists.txt
    │   ├── source1.cpp
    │   └── ...
    └── ...
```

1. **Root `CMakeLists.txt`:**

```cmake
cmake_minimum_required(VERSION 3.10)
project(MyProject)

# Include subdirectories
add_subdirectory(src)
add_subdirectory(lib)
```

1. **`src/CMakeLists.txt`:**

```cmake
# Add all source files in this directory to the executable
add_executable(MyExecutable main.cpp)

# Include the header files from the include directory
target_include_directories(MyExecutable PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/../include)
```

1. **`lib/CMakeLists.txt`:**

```cmake
# Add each library as a subproject
add_subdirectory(library1)
# Add more libraries if needed
```

1. **`lib/library1/CMakeLists.txt`:**

```cmake
# Add all source files in this directory to the library
add_library(library1 source1.cpp)

# Include the header files from the include directory
target_include_directories(library1 PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/../../include)
```

This structure assumes you have source files in the `src` directory, headers in the `include` directory, and libraries in the `lib` directory. Adjust the paths and names according to your project's structure.

Each directory contains its own `CMakeLists.txt` file to manage its specific build targets. Subdirectories are added using `add_subdirectory()` in the root `CMakeLists.txt`. You can include headers from the `include` directory using `target_include_directories()` to ensure they are available for compilation.

### 1. Alternative Project Strucutre

Certainly! CMake is a popular tool used for building, testing, and packaging software projects. Below is an example of an alternative project structure using CMake:

```bash
project_name/
│
├── CMakeLists.txt
├── src/
│   ├── CMakeLists.txt
│   ├── main.cpp
│   ├── module1/
│   │   ├── CMakeLists.txt
│   │   ├── module1.cpp
│   │   └── module1.h
│   └── module2/
│       ├── CMakeLists.txt
│       ├── module2.cpp
│       └── module2.h
│
├── include/
│   ├── module1/
│   │   └── module1.h
│   └── module2/
│       └── module2.h
│
└── test/
    ├── CMakeLists.txt
    ├── test_module1.cpp
    └── test_module2.cpp
```

Let's break down the structure:

- `CMakeLists.txt`: The main CMakeLists file for the project.
- `src/`: Directory containing the source code of the project.
  - `CMakeLists.txt`: CMakeLists file for the source directory.
  - `main.cpp`: Main entry point of the application.
  - `module1/` and `module2/`: Directories for different modules of the project.
    - `CMakeLists.txt`: CMakeLists files for each module.
    - `module1.cpp` and `module2.cpp`: Source files for each module.
    - `module1.h` and `module2.h`: Header files for each module.
- `include/`: Directory containing public headers for the project.
  - `module1/` and `module2/`: Directories for headers of each module.
- `test/`: Directory containing test code.
  - `CMakeLists.txt`: CMakeLists file for the test directory.
  - `test_module1.cpp` and `test_module2.cpp`: Test files for each module.

Example `CMakeLists.txt` for the project:

```cmake
cmake_minimum_required(VERSION 3.5)
project(project_name)

# Include directories
include_directories(include)

# Add subdirectories
add_subdirectory(src)
add_subdirectory(test)
```

Example `src/CMakeLists.txt`:

```cmake
# Module 1
add_subdirectory(module1)

# Module 2
add_subdirectory(module2)

# Main executable
add_executable(main main.cpp)
target_link_libraries(main module1 module2)
```

Example `test/CMakeLists.txt`:

```cmake
# Test Module 1
add_executable(test_module1 test_module1.cpp)
target_link_libraries(test_module1 module1)

# Test Module 2
add_executable(test_module2 test_module2.cpp)
target_link_libraries(test_module2 module2)
```

This structure separates source code, public headers, and test code, making the project organized and maintainable.

### 1. Variables and Options

In CMake, variables and options play crucial roles in configuring and building software projects. They allow developers to customize the build process, control compiler flags, specify paths, and more. Here's an overview of variables and options in CMake:

#### Variables

1. **CMake Variables:**
   These are variables defined within CMakeLists.txt files or via the command line using `-D` option with cmake. They can be set, modified, and queried within CMake scripts.

2. **Environment Variables:**
   Environment variables set in the shell where CMake is executed can also influence the behavior of CMake scripts. For example, `CC` and `CXX` environment variables can specify the C and C++ compilers, respectively.

3. **Cache Variables:**
   Cache variables are persistent across CMake runs and can be set using the `-D` option during the initial configuration phase. They are stored in the CMakeCache.txt file and can be modified using `ccmake`, `cmake-gui`, or by directly editing the cache file.

#### Options

1. **Boolean Options:**
   These are options that can be turned on or off, typically with values like `ON` or `OFF`. They can control various build features or configurations.

2. **String Options:**
   Options that accept string values, which can be used to specify paths, compiler flags, or other string-based configuration options.

#### How They Are Used

1. **Configuring Build:**
   Variables and options are used to configure the build process, such as specifying compiler flags, defining installation paths, enabling/disabling features, etc.

2. **Conditional Compilation:**
   They are often used in conditional statements within CMake scripts to control compilation based on certain conditions or requirements.

3. **Cross-Platform Compatibility:**
   Variables and options help maintain cross-platform compatibility by allowing different configurations for different platforms or compiler toolchains.

#### Example

```cmake
# Setting variables
set(MY_VARIABLE "some_value")

# Setting options
option(ENABLE_FEATURE_X "Enable feature X" ON)

# Using variables and options
if(ENABLE_FEATURE_X)
    add_definitions(-DFEATURE_X_ENABLED)
endif()

# Printing variables
message("Value of MY_VARIABLE: ${MY_VARIABLE}")
```

#### Command Line Usage

- To set variables/options via command line:

  ```bash
  cmake -DMY_VARIABLE="value" -DENABLE_FEATURE_X=ON ..
  ```

- To view and modify cache variables using `ccmake`:

  ```bash
  ccmake ..
  ```

- To configure and generate build files:

  ```bash
  cmake ..
  ```

Variables and options in CMake provide a flexible and powerful way to customize the build process and tailor it to specific requirements. They are integral to creating maintainable and portable CMake-based projects.

### 1. Configure File

To configure a `CMakeLists.txt` file, you need to define the project, its dependencies, any custom settings, and options for building the project. Below is a basic example of a `CMakeLists.txt` file:

```cmake
cmake_minimum_required(VERSION 3.0)  # Specify the minimum CMake version required

# Define the project and its languages
project(MyProject LANGUAGES CXX)

# Set any compiler flags or options
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Add any dependencies using find_package or include_directories
find_package(Boost REQUIRED)

# Set sources for the project
set(SOURCES 
    src/main.cpp
    src/foo.cpp
)

# Add executable target
add_executable(MyExecutable ${SOURCES})

# Link any required libraries
target_link_libraries(MyExecutable PRIVATE Boost::boost)
```

In this example:

- `cmake_minimum_required`: Specifies the minimum version of CMake required to configure the project.
- `project`: Defines the project name and specifies the languages used in the project.
- `set`: Sets any variables, such as compiler flags or standards.
- `find_package`: Searches for dependencies. Here, it's searching for Boost.
- `set(SOURCES ...)`: Defines the source files for the project.
- `add_executable`: Creates an executable target from the defined source files.
- `target_link_libraries`: Specifies any libraries that need to be linked with the target executable.

You can add more advanced configurations based on your project's needs, such as including additional directories, setting compile definitions, enabling testing, etc. The `CMake` documentation is a great resource for learning more about its capabilities and syntax.

### 1. Sources and Headers

In CMake, when you're working on a project that consists of multiple source files and header files, you need to organize them properly to ensure that they are compiled and linked correctly. Here's a basic example of how you might structure your CMakeLists.txt file to handle sources and headers:

```cmake
cmake_minimum_required(VERSION 3.0)
project(MyProject)

# Add all your source files
set(SOURCES 
    src/main.cpp
    src/foo.cpp
    src/bar.cpp
)

# Add all your header files
set(HEADERS
    include/foo.h
    include/bar.h
)

# Add include directories
include_directories(include)

# Create executable from sources
add_executable(MyExecutable ${SOURCES} ${HEADERS})
```

In this example:

- `set(SOURCES ...)` lists all the source files (*.cpp) that are part of your project.
- `set(HEADERS ...)` lists all the header files (*.h) that are part of your project.
- `include_directories(include)` specifies the directory where header files are located. This is necessary so that the compiler can find the header files when compiling the source files.
- `add_executable(MyExecutable ${SOURCES} ${HEADERS})` creates an executable named `MyExecutable` from the source files listed in `SOURCES` and `HEADERS`. CMake automatically handles compiling and linking these files into the final executable.

Make sure to adjust the paths and filenames to match your project's structure. Additionally, consider using CMake features like `target_include_directories()` and `target_sources()` for more fine-grained control over source and header file organization, especially in larger projects.

### 1. External Libraries: Git Submodule

Using Git submodules in conjunction with CMake is a common approach to manage external libraries within a CMake project. Git submodules allow you to include another Git repository as a subdirectory within your main repository. This is useful for integrating third-party libraries into your project while maintaining version control and managing dependencies.

Here's a general guide on how to use Git submodules with CMake:

1. **Add the Submodule**:
   First, you need to add the external library repository as a submodule to your main project repository. You can do this using the following command:

   ```bash
   git submodule add <repository_url> <submodule_directory>
   ```

   Replace `<repository_url>` with the URL of the external library repository and `<submodule_directory>` with the directory where you want to place the submodule within your project.

2. **Update Submodules**:
   After adding the submodule, you need to initialize and update it to fetch the submodule contents.

   ```bash
   git submodule init
   git submodule update
   ```

3. **Use Submodule in CMake**:
   Now that you have the submodule in your project directory, you can use it in your CMakeLists.txt file. You'll typically want to add the submodule's directory to your project and then use it as needed. Here's a basic example:

   ```cmake
   # Add the submodule directory to the build
   add_subdirectory(<submodule_directory>)

   # Link the submodule library to your main project
   target_link_libraries(<your_project_target> PUBLIC <submodule_library>)
   ```

   Replace `<submodule_directory>` with the path to your submodule directory and `<submodule_library>` with the name of the library provided by the submodule.

4. **Building Your Project**:
   When you build your project with CMake, it will automatically include and build the submodule along with your main project.

5. **Updating Submodules**:
   If the external library repository is updated, you can fetch the changes into your project by running:

   ```bash
   git submodule update --remote
   ```

   This command will update the submodule to the latest commit of the branch it is tracking.

Using Git submodules with CMake allows you to manage external dependencies efficiently while keeping your project organized and maintainable. Make sure to document the external dependencies and their usage in your project's documentation or README file for clarity to other developers.

### 1. Dependency Graph

CMake itself doesn't provide direct visualization of dependency graphs, but it does generate dependency information that can be used to create such graphs. CMake is primarily a build system generator, and it generates build scripts (like Makefiles or project files for IDEs) based on the specifications provided in the CMakeLists.txt files.

To understand dependencies in a CMake project, you can examine the CMakeLists.txt files in each directory. Dependencies are typically declared using `target_link_libraries()` and `target_include_directories()` commands.

However, to visualize the dependency graph of your project, you might need to use additional tools or scripts. Here are some approaches you could take:

1. **CMake-Dependent Targets**: CMake 3.7 and later versions introduced a feature where you can query the dependencies of a target. This can be helpful in understanding the dependencies within your project. For example:

    ```cmake
    get_target_property(dependencies my_target INTERFACE_LINK_LIBRARIES)
    message(STATUS "Dependencies of my_target: ${dependencies}")
    ```

    This command will give you a list of dependencies for the target `my_target`.

2. **cmake-graphviz**: There's a project called `cmake-graphviz` which parses CMake files to generate a Graphviz (.dot) file representing the dependency graph of targets in your project. You can then use Graphviz tools to visualize the graph. You can find the project [here](https://github.com/ChicagoDave/cmake-graphviz).

3. **Custom Scripts**: You can write custom scripts to parse CMakeLists.txt files and extract dependency information to generate a visual representation using tools like Graphviz or any other graph visualization library.

4. **IDE Integration**: Some IDEs provide visualization of CMake project structures and dependencies. For example, CLion has built-in support for visualizing CMake project structure and dependencies.

5. **Manual Inspection**: For smaller projects, or if you just need a quick overview, manually inspecting CMakeLists.txt files might be sufficient. By looking at the `target_link_libraries()` and `target_include_directories()` commands, you can infer dependencies.

6. **cmake-ide**: If you are using Emacs, there's a package called `cmake-ide` which can assist in navigating CMake projects. While it doesn't directly provide visualization, it can help in understanding dependencies within the Emacs environment.

Choose the approach that best suits your needs and preferences based on the size and complexity of your project, as well as the tools and libraries you're comfortable with.

### 1. External Libraries: Fetch Content

In CMake, the `FetchContent` module is used to download and include external projects or libraries directly into your CMake project. This is particularly useful when you want to manage dependencies within your project repository without relying on external package managers or having to manually include source code.

Here's a basic example of how you might use `FetchContent` to include an external library in your CMake project:

```cmake
cmake_minimum_required(VERSION 3.11)
project(MyProject)

include(FetchContent)

# Define the URL and the tag/commit hash of the external library
set(EXTERNAL_LIBRARY_URL "https://example.com/external_library.git")
set(EXTERNAL_LIBRARY_TAG "v1.2.3")  # Replace with the appropriate tag or commit hash

# Fetch the external library
FetchContent_Declare(
    ExternalLibrary
    GIT_REPOSITORY ${EXTERNAL_LIBRARY_URL}
    GIT_TAG ${EXTERNAL_LIBRARY_TAG}
)

FetchContent_GetProperties(ExternalLibrary)
if(NOT ExternalLibrary_POPULATED)
    FetchContent_Populate(ExternalLibrary)
    add_subdirectory(${ExternalLibrary_SOURCE_DIR} ${ExternalLibrary_BINARY_DIR})
endif()

# Now you can use the imported targets provided by the external library
# For example, if it's a library named "ExternalLibrary", you can link against it
target_link_libraries(MyProject PRIVATE ExternalLibrary)
```

In this example:

- We specify the URL of the external library's Git repository and the tag or commit hash that we want to use.
- We use `FetchContent_Declare()` to declare the external library. This sets up the parameters for fetching it.
- We use `FetchContent_GetProperties()` to check if the content has already been populated.
- If it's not populated, we use `FetchContent_Populate()` to download and populate the content.
- Finally, we can link against the imported targets provided by the external library, allowing us to use its functionality in our project.

This approach simplifies the process of including external libraries in your CMake project, making it easier to manage dependencies.

### 1. Doxygen Documenation

To generate Doxygen documentation using CMake, you'll typically follow these steps:

1. **Install Doxygen**: Make sure you have Doxygen installed on your system. You can download and install it from the [official website](http://www.doxygen.nl/download.html) or use your system's package manager.

2. **Write a Doxyfile**: Doxygen uses a configuration file called `Doxyfile` to specify how documentation should be generated. You can create a `Doxyfile` manually or let Doxygen generate one for you by running `doxygen -g`.

3. **Configure CMake to Generate Documentation**: You'll need to add commands to your `CMakeLists.txt` to generate the documentation when building your project. Here's a basic example:

   ```cmake
   find_package(Doxygen)

   if(DOXYGEN_FOUND)
       set(DOXYGEN_IN ${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile)
       set(DOXYGEN_OUT ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile)

       configure_file(${DOXYGEN_IN} ${DOXYGEN_OUT} @ONLY)

       add_custom_target(doc_doxygen
           COMMAND ${DOXYGEN_EXECUTABLE} ${DOXYGEN_OUT}
           WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
           COMMENT "Generating Doxygen documentation"
           VERBATIM
       )

       # Add doc_doxygen as dependency to build all documents when calling "make all"
       add_dependencies(doc_all doc_doxygen)
   else()
       message("Doxygen not found, cannot generate documentation")
   endif()
   ```

   This script checks if Doxygen is installed on the system and, if found, configures a custom target to generate documentation using the `Doxyfile`.

4. **Run CMake and Build**: After adding the above configuration to your `CMakeLists.txt`, run CMake as usual:

   ```bash
   cmake -B build
   ```

   Then build your project using your preferred build tool (e.g., `make` for Unix-like systems):

   ```bash
   cmake --build build
   ```

5. **Generate Documentation**: Once you've built your project, you can generate the documentation by running the custom target:

   ```bash
   cmake --build build --target doc_doxygen
   ```

   This will invoke Doxygen with the generated `Doxyfile` and create the documentation.

6. **View Documentation**: After the documentation has been generated, you can find it in the specified output directory (usually specified in the `Doxyfile`). Open the generated HTML files in a web browser to view your documentation.

Remember to customize the `Doxyfile` according to your project's needs, especially the input and output directories, and any other settings you may require.

### 1. Public, Interface and Private

In CMake, when you're creating a library target, you often use the `target_include_directories`, `target_compile_definitions`, and other `target_*` commands to specify various properties for your target. These properties can be specified for different scopes: `PUBLIC`, `INTERFACE`, and `PRIVATE`.

Here's what each of these scopes means:

1. **PUBLIC**: When you set a property to `PUBLIC`, it means that this property will be applied to the target itself, any targets that link to it, and any targets that link to those targets transitively.

2. **INTERFACE**: When you set a property to `INTERFACE`, it means that this property will be applied to any targets that link to the target but not to the target itself. It's useful when you want to specify properties that only affect users of your library but not the implementation of the library itself.

3. **PRIVATE**: When you set a property to `PRIVATE`, it means that this property will be applied only to the target itself and will not affect targets that link to it. This is useful for specifying properties that are only relevant to the implementation of the target and should not be propagated to targets linking to it.

Here's an example to illustrate these concepts:

```cmake
# Create a library target
add_library(mylib STATIC mylib.cpp)

# Include directories for the target and its users
target_include_directories(mylib PUBLIC include)
target_include_directories(mylib PRIVATE src)

# Define compile definitions
target_compile_definitions(mylib PUBLIC MYLIB_ENABLE_FEATURE_A)
target_compile_definitions(mylib PRIVATE MYLIB_ENABLE_FEATURE_B)

# Link libraries
target_link_libraries(mylib PUBLIC some_other_library)

# If someone links to mylib, they will automatically include 'include'
# directory and MYLIB_ENABLE_FEATURE_A definition, but not MYLIB_ENABLE_FEATURE_B
# If someone links to mylib, they will also link to 'some_other_library'
# mylib itself will have 'src' directory included and MYLIB_ENABLE_FEATURE_B defined
```

In this example, `include` directory and the `MYLIB_ENABLE_FEATURE_A` definition are `PUBLIC`, which means any target linking to `mylib` will also inherit these properties. The `src` directory and the `MYLIB_ENABLE_FEATURE_B` definition are `PRIVATE`, meaning they are only relevant to `mylib` itself and won't affect its users.

### 1. Adding Compiler Warnings

In CMake, adding compiler warnings can be done by setting appropriate flags for your target compiler. Here's a basic example of how you can add compiler warnings using CMake:

```cmake
# Set CMake minimum required version
cmake_minimum_required(VERSION 3.0)

# Project name
project(MyProject)

# Add executable
add_executable(my_executable main.cpp)

# Set compiler-specific warning flags
if (CMAKE_CXX_COMPILER_ID MATCHES "Clang" OR CMAKE_COMPILER_IS_GNUCXX)
    target_compile_options(my_executable PRIVATE -Wall -Wextra -Wpedantic)
elseif (CMAKE_CXX_COMPILER_ID STREQUAL "MSVC")
    target_compile_options(my_executable PRIVATE /W4)
endif ()
```

In this example:

- `add_executable()` adds your executable target (replace `main.cpp` with your actual source files).
- `target_compile_options()` is used to set compiler options specifically for your target executable.
- The `PRIVATE` keyword makes sure that these options are only applied to `my_executable` and not propagated to other targets.
- Compiler-specific warning flags are set based on the compiler being used. For example:
  - For Clang or GCC, `-Wall`, `-Wextra`, and `-Wpedantic` are commonly used warning flags.
  - For MSVC, `/W4` enables a high level of warning messages.

You can adjust these warning flags according to your project's requirements and the level of strictness you desire.

### 1. Sanitizers

Sanitizers in CMake refer to a set of compiler flags and runtime libraries provided by tools like AddressSanitizer, UndefinedBehaviorSanitizer, ThreadSanitizer, and MemorySanitizer. These tools are aimed at detecting various types of bugs in C and C++ code, such as memory leaks, buffer overflows, use-after-free errors, etc.

To enable sanitizers in CMake, you typically need to modify your CMakeLists.txt file to include the appropriate flags and settings. Here's a basic example of how you can enable AddressSanitizer using CMake:

```cmake
cmake_minimum_required(VERSION 3.1)
project(MyProject)

# Enable AddressSanitizer
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fsanitize=address -fno-omit-frame-pointer")

# Add your project files and executables
add_executable(my_executable main.cpp)
```

In this example, `-fsanitize=address` enables AddressSanitizer, which helps catch memory errors like use-after-free and buffer overflows. The `-fno-omit-frame-pointer` flag is recommended to provide better stack traces.

You can similarly enable other sanitizers by replacing `address` with `undefined`, `thread`, or `memory`, depending on the type of sanitizer you want to use.

Remember that sanitizers slow down your code because they add runtime checks, and they may also increase memory consumption. However, they are incredibly useful during development to catch bugs early, especially in complex codebases.

When building your project with CMake after including such configurations, the compiler will apply the specified sanitizers, and any runtime errors detected by the sanitizers will be reported during execution.

### 1. What is the IPO/LTO?

In programming, IPO/LTO can stand for two different concepts:

1. **Input-Process-Output (IPO)**: This is a fundamental concept in computer science and software engineering that describes the flow of data within a computer program or a system. It represents the basic structure of how a program operates:
   - **Input**: Data or information received by the program from external sources, such as user input, sensors, files, or network communication.
   - **Process**: The manipulation, calculation, or transformation of the input data by the program according to its algorithms and logic.
   - **Output**: The result or outcome produced by the program, which could be displayed to the user, saved to a file, sent over a network, or used as input for further processing.

2. **Link-Time Optimization (LTO)**: This is a compiler optimization technique used in software development, especially in languages like C and C++, where optimization decisions are deferred until the linking phase of building the executable. Traditionally, optimization is performed by the compiler during compilation. However, with LTO, the compiler produces intermediate representations (IR) of the code and passes it to the linker. The linker can then perform global optimization across all the translation units before generating the final executable. LTO can result in better optimization opportunities by allowing the compiler to make more informed decisions based on the entire program's context.

These two concepts are distinct but crucial in the realm of programming and software development.

### 1. IPO/LTO in CMake

In the context of CMake, IPO (Interprocedural Optimization) and LTO (Link Time Optimization) are techniques used to optimize the performance of compiled code. Here's how you can enable them in your CMake project:

1. **Interprocedural Optimization (IPO)**:

IPO involves optimizing the entire program across multiple source files. This optimization can result in better performance by allowing the compiler to make optimizations that would not be possible if each source file were compiled separately.

To enable IPO in CMake, you typically need to set compiler-specific flags. For example, for GCC and Clang, you can use the `-flto` flag:

```cmake
if(CMAKE_COMPILER_IS_GNUCC OR CMAKE_COMPILER_IS_GNUCXX)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -flto")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -flto")
endif()
```

For Visual Studio, you can use `/GL` (Whole Program Optimization) flag:

```cmake
if(MSVC)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} /GL")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /GL")
endif()
```

1. **Link Time Optimization (LTO)**:

LTO involves performing optimizations during the linking stage of the compilation process. This allows the linker to optimize across object files and libraries, resulting in potentially better performance.

To enable LTO, you typically need to set linker flags. For GCC and Clang, you can use the `-flto` flag during both compilation and linking:

```cmake
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -flto")
```

For Visual Studio, you can use `/LTCG` (Link-Time Code Generation) flag:

```cmake
if(MSVC)
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} /LTCG")
endif()
```

It's worth noting that enabling IPO and LTO can significantly increase compilation time and may require more memory during the build process. However, the resulting executable may have better performance.

Remember to test your application thoroughly after enabling these optimizations to ensure that they don't introduce any unexpected behavior or bugs. Additionally, not all compilers and platforms support IPO and LTO, so make sure to check the documentation for your specific compiler and version.

### 1. External Libraries: CPM

CPM (CMake Package Manager) is a modern approach to handling external dependencies in CMake-based projects. It aims to simplify the process of integrating external libraries into CMake projects without requiring additional build steps or complex setup.

Here's a basic overview of how you can use CPM to integrate external libraries into your CMake project:

1. **Include CPM**: First, you need to include CPM in your CMake project. This can be done by adding the following lines to your CMakeLists.txt file:

    ```cmake
    include(cmake/CPM.cmake)
    ```

    You also need to make sure that the `CPM.cmake` file is present in the `cmake` directory within your project.

2. **Define Dependencies**: Next, you can define the dependencies you want to include in your project using the `CPMAddPackage` function. For example:

    ```cmake
    CPMAddPackage(
        NAME MyLibrary
        GIT_REPOSITORY https://github.com/username/my-library.git
        VERSION 1.2.3
    )
    ```

    This will fetch the `MyLibrary` from the specified Git repository at version 1.2.3 and make it available for use in your project.

3. **Use the Library**: Once the library is added, you can use it in your CMakeLists.txt file as you would with any other library. For example:

    ```cmake
    target_link_libraries(MyExecutable PRIVATE MyLibrary)
    ```

    This will link the `MyLibrary` to your executable named `MyExecutable`.

4. **Build**: Finally, you can build your project using CMake as usual.

    ```bash
    cmake .
    make
    ```

    CPM will automatically download and configure the specified dependencies during the configuration step.

Using CPM simplifies the process of managing dependencies in CMake projects by handling the download, configuration, and integration of external libraries automatically. This can help streamline the development process and make it easier to maintain CMake projects with multiple dependencies.

### 1. External Libraries: Conan

CMake is a popular cross-platform build system used to manage the build process of software projects. Conan, on the other hand, is a C/C++ package manager that allows developers to easily manage dependencies for their projects.

When using external libraries with CMake and Conan, you typically follow these steps:

1. **Install Conan**: First, you need to install Conan if you haven't already. You can do this via pip (Python package manager) by running:

   ```bash
   pip install conan
   ```

2. **Create a Conanfile**: In your project directory, create a `Conanfile.txt` or `Conanfile.py` where you specify the dependencies required by your project along with their versions.

3. **Run Conan Install**: Run the following command in your project directory to let Conan fetch and install the dependencies specified in your Conanfile:

   ```bash
   conan install .
   ```

4. **Integrate Conan with CMake**: You need to integrate Conan with CMake to make use of the dependencies it installed. This can be done using the `conan_basic_setup()` command provided by the Conan CMake integration.

   ```cmake
   include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
   conan_basic_setup(TARGETS)
   ```

   The `conan_basic_setup()` function will define imported targets for each dependency, which can then be used in your CMake project.

5. **Link Dependencies**: Finally, in your CMakeLists.txt file, you can link the imported Conan targets to your executable or library targets using the `target_link_libraries()` command.

   ```cmake
   target_link_libraries(your_executable_or_library CONAN_PKG::package1 CONAN_PKG::package2)
   ```

Replace `package1`, `package2`, etc., with the names of the packages you installed via Conan.

By following these steps, you can easily manage external libraries with Conan and integrate them into your CMake project. This setup provides a clean and efficient way to handle dependencies in your C/C++ projects.

### 1. External Libraries: VCPKG

CMake is a cross-platform build system generator widely used for C and C++ projects. When it comes to integrating external libraries into your CMake project, Vcpkg can be a valuable tool.

Vcpkg is an open-source package manager for C and C++ libraries, developed by Microsoft. It simplifies the process of acquiring and building open-source libraries on Windows, Linux, and macOS.

Here's how you can use Vcpkg with CMake to integrate external libraries into your project:

1. **Install Vcpkg**: Begin by installing Vcpkg on your system. You can find instructions for installation on the [Vcpkg GitHub repository](https://github.com/microsoft/vcpkg).

2. **Install Libraries**: Once Vcpkg is installed, you can use it to install the libraries you need for your project. For example, to install the Boost C++ libraries, you would run:

   ```bash
   vcpkg install boost
   ```

3. **Integrate with CMake**: Now, you need to let CMake know where to find the libraries you've installed with Vcpkg. This is typically done by setting the `CMAKE_TOOLCHAIN_FILE` variable to point to Vcpkg's `scripts/buildsystems/vcpkg.cmake` file. You can do this either through your CMakeLists.txt file or through the command line when invoking CMake.

   Here's an example of how you might set it in your CMakeLists.txt:

   ```cmake
   set(CMAKE_TOOLCHAIN_FILE "<path_to_vcpkg>/scripts/buildsystems/vcpkg.cmake" CACHE STRING "")
   ```

   Replace `<path_to_vcpkg>` with the actual path to your Vcpkg installation.

4. **Specify Dependencies**: Finally, in your CMakeLists.txt file, you can specify the libraries your project depends on using the `target_link_libraries()` function. CMake will automatically find these libraries through Vcpkg.

   ```cmake
   cmake_minimum_required(VERSION 3.0)
   project(MyProject)

   # Add executable
   add_executable(MyExecutable main.cpp)

   # Link libraries
   target_link_libraries(MyExecutable PRIVATE boost)
   ```

   Replace `boost` with the name of the library you want to link against.

5. **Build Your Project**: With the above configurations in place, you can now build your project using CMake. When you run `cmake` and `make` (or equivalent), CMake will automatically locate the libraries installed by Vcpkg and link them with your project.

By following these steps, you can effectively use Vcpkg with CMake to manage external library dependencies in your C++ projects.

### 1. Which Tool for external Libraries?

When working with external libraries in a CMake-based project, you have several options for integrating them into your build process. The choice of tool depends on various factors such as the complexity of the library, its build system, and the requirements of your project. Here are some common tools and approaches:

1. **Find Package**: Many popular libraries provide CMake support through `Find<Library>.cmake` modules. These modules are typically distributed with CMake or the library itself. You can use the `find_package()` command in your CMakeLists.txt to locate and configure the library. For example:

    ```cmake
    find_package(OpenCV REQUIRED)
    include_directories(${OpenCV_INCLUDE_DIRS})
    target_link_libraries(my_executable ${OpenCV_LIBS})
    ```

    This approach is suitable for libraries that support CMake and provide Find modules.

2. **pkg-config**: If the library supports `pkg-config`, you can use the `find_package(PkgConfig)` module in CMake to locate and configure it. This approach is common for libraries in the Linux ecosystem.

    ```cmake
    find_package(PkgConfig REQUIRED)
    pkg_search_module(LIBRARY_NAME REQUIRED library)
    include_directories(${LIBRARY_NAME_INCLUDE_DIRS})
    target_link_libraries(my_executable ${LIBRARY_NAME_LIBRARIES})
    ```

3. **ExternalProject_Add**: If the library doesn't provide CMake support, you can use `ExternalProject_Add()` command to download, configure, build, and install the library as part of your CMake build process. This approach is suitable for integrating third-party libraries with non-CMake build systems.

    ```cmake
    include(ExternalProject)
    ExternalProject_Add(
        library_name
        URL <URL_TO_LIBRARY_SOURCE>
        PREFIX ${CMAKE_BINARY_DIR}/library_name
        CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${CMAKE_BINARY_DIR}/install
    )
    include_directories(${CMAKE_BINARY_DIR}/install/include)
    target_link_directories(my_executable PRIVATE ${CMAKE_BINARY_DIR}/install/lib)
    target_link_libraries(my_executable library_name)
    ```

4. **FetchContent**: Introduced in CMake 3.11, `FetchContent` allows you to include external projects directly into your CMakeLists.txt without the need for separate `ExternalProject_Add()` calls. This approach simplifies the integration of external dependencies.

    ```cmake
    include(FetchContent)
    FetchContent_Declare(
        library_name
        URL <URL_TO_LIBRARY_SOURCE>
    )
    FetchContent_MakeAvailable(library_name)
    include_directories(${library_name_SOURCE_DIR}/include)
    target_link_libraries(my_executable library_name)
    ```

Each of these methods has its pros and cons, so the best approach depends on the specific requirements of your project and the characteristics of the external library you're integrating.

5. **Manual Configuration**: In some cases, you may need to manually specify the include directories and library paths for the external library.

   ```cmake
   include_directories(/path/to/library/include)
   link_directories(/path/to/library/lib)
   target_link_libraries(my_executable library_name)
   ```

Choose the appropriate method based on the availability of CMake configuration files provided by the external library and your project's specific requirements.

### 1. Final Github Repository

Creating a GitHub repository for your CMake project involves a few steps. Assuming you already have a local project that you want to push to GitHub, here's a general guide:

1. **Create a new repository on GitHub:**
   - Go to https://github.com/.
   - Log in to your account.
   - Click on the "+" icon in the top right corner and select "New repository".
   - Fill in the repository name, description, choose whether it should be public or private, and other settings as needed.
   - Click on "Create repository".

2. **Initialize your local repository:**
   - If you haven't already done so, initialize Git in your project directory:

     ```bash
     git init
     ```

   - Add your files to the repository:

     ```bash
     git add .
     ```

   - Commit your changes:

     ```bash
     git commit -m "Initial commit"
     ```

3. **Link your local repository to the GitHub repository:**
   - Copy the URL of your GitHub repository (should be something like `https://github.com/your-username/your-repo.git`).
   - Add the GitHub repository as the remote origin:

     ```bash
     git remote add origin <GitHub repository URL>
     ```

   - Verify that the remote origin is set correctly:

     ```bash
     git remote -v
     ```

4. **Push your code to GitHub:**
   - Push your code to the GitHub repository:

     ```bash
     git push -u origin master
     ```

     This command will push your code to the master branch. If you are using a different branch, replace `master` with the name of your branch.

5. **Verify on GitHub:**
   - Go back to your GitHub repository page and refresh it. You should see your code there.

That's it! Your CMake project is now hosted on GitHub. Remember to update your `.gitignore` file to exclude any build artifacts or sensitive information before committing and pushing your code.

### 1. CMake Scripts

CMake is a cross-platform build system generator widely used for C and C++ projects. It allows developers to describe the build process for their software in a platform-independent way, generating native build scripts (e.g., Makefiles on Unix-like systems, Visual Studio projects on Windows) based on a high-level CMakeLists.txt configuration file.

Here's a basic example of a CMakeLists.txt script:

```cmake
# Set the minimum required version of CMake
cmake_minimum_required(VERSION 3.10)

# Set the project name and version
project(MyProject VERSION 1.0)

# Define sources
set(SOURCES
    src/main.cpp
    src/foo.cpp
    src/bar.cpp
)

# Add an executable target
add_executable(my_executable ${SOURCES})

# Specify include directories
target_include_directories(my_executable PUBLIC include)

# Set compiler flags
target_compile_options(my_executable PRIVATE -Wall -Wextra)

# Set compiler features
target_compile_features(my_executable PUBLIC cxx_std_11)
```

In this script:

- `cmake_minimum_required`: Specifies the minimum required version of CMake.
- `project`: Sets the project name and version.
- `set`: Defines variables (e.g., SOURCES).
- `add_executable`: Creates an executable target from source files.
- `target_include_directories`: Specifies include directories for the target.
- `target_compile_options`: Sets compiler options for the target.
- `target_compile_features`: Specifies the required language features for the target.

This is just a basic example. CMake provides many more commands and options for configuring builds, such as specifying dependencies, setting compiler flags, configuring installation rules, enabling testing, and more.

CMake scripts are highly customizable and can be tailored to suit the specific needs of your project. They allow for fine-grained control over the build process while maintaining platform independence.

### 1. Clang-Tidy

Clang-Tidy is a powerful tool for analyzing C++ code and suggesting improvements. Integrating it into a CMake-based project involves a few steps. Here's a basic guide on how to do it:

1. **Install Clang-Tidy**: First, ensure you have Clang-Tidy installed on your system. You can install it via package managers like apt or brew, or you can build it from source.

2. **Configure CMakeLists.txt**: Modify your `CMakeLists.txt` file to include Clang-Tidy checks during the build process. You'll typically want to enable Clang-Tidy for specific build targets. Here's an example of how you can do this:

    ```cmake
    # Enable Clang-Tidy
    set(CMAKE_CXX_CLANG_TIDY "clang-tidy;-checks=*")

    # Add your executable or library
    add_executable(your_executable main.cpp)
    ```

    Replace `your_executable` with the name of your target. The `set(CMAKE_CXX_CLANG_TIDY ...)` line specifies the Clang-Tidy checks you want to run. In this example, `*` means all checks. You can specify specific checks based on your project's needs.

3. **Build Your Project**: Once you've configured your `CMakeLists.txt` file, build your project as usual using CMake. Clang-Tidy will be invoked during the build process, and any issues it finds will be displayed in the build output.

4. **Customizing Clang-Tidy Checks**: You can customize Clang-Tidy checks further by specifying specific checks or disabling certain checks. For example:

    ```cmake
    set(CMAKE_CXX_CLANG_TIDY "clang-tidy;-checks=bugprone-*,performance-*,clang-analyzer-*")
    ```

    This will enable specific subsets of checks related to bug-prone code, performance, and clang-analyzer checks.

5. **Ignoring Files or Directories**: Sometimes you may want to exclude certain files or directories from Clang-Tidy checks. You can do this by modifying the `CMakeLists.txt` file:

    ```cmake
    set_directory_properties(PROPERTIES
        ADDITIONAL_CLEAN_FILES "directory/to/exclude/"
    )
    ```

    This will exclude the specified directory from Clang-Tidy checks.

6. **Running Clang-Tidy Directly**: If you want to run Clang-Tidy directly without building your project, you can do so using the command line:

    ```bash
    clang-tidy your_source_file.cpp -- -I/path/to/your/includes
    ```

    This command will run Clang-Tidy on `your_source_file.cpp`, and you can specify additional include directories with `-I`.

Integrating Clang-Tidy into your CMake-based project can help improve code quality and catch potential issues early in the development process.

### 1. Clang-Format and Cmake-Format

As of my last update in January 2022, `clang-format` and `cmake-format` are two separate tools serving different purposes in the development workflow.

1. **Clang-Format**:
   - `clang-format` is a tool developed as part of the LLVM project. It's primarily used for formatting C, C++, and other compatible language code according to a defined style.
   - It can be configured to follow various coding styles such as Google, LLVM, Chromium, etc.
   - `clang-format` can be integrated into various IDEs or text editors to automatically format code on save or on demand.
   - It's particularly useful in enforcing consistent code style across a codebase, especially in collaborative projects.

2. **CMake-Format**:
   - `cmake-format`, on the other hand, is specifically designed for formatting CMake scripts.
   - CMake is a popular cross-platform build system, and `cmake-format` helps in maintaining consistent formatting within CMakeLists.txt files.
   - Similar to `clang-format`, `cmake-format` allows for customization of formatting rules to fit specific project or team preferences.
   - It's particularly useful in maintaining readability and consistency in CMake scripts, which can become quite complex in large projects.

While `clang-format` and `cmake-format` serve different purposes, they both contribute to improving code quality and maintainability through consistent formatting. Integrating them into development workflows can help streamline the coding process and ensure adherence to coding standards.

### 1. Github Pages

To host documentation generated by CMake on GitHub Pages, you can follow these general steps:

1. **Generate Documentation**: First, generate the documentation for your project using CMake. CMake can generate documentation using tools like Doxygen, Sphinx, or others. You need to set up the CMake configuration to generate documentation during the build process.

2. **Configure GitHub Pages**: If you haven't already, set up GitHub Pages for your repository. Go to your repository settings and choose the `Pages` tab. Select the branch you want to use for GitHub Pages (typically `main` or `master`) and the folder from which to serve your documentation.

3. **Commit Documentation**: After generating the documentation, commit the generated files to your repository. Make sure you're committing to the branch configured for GitHub Pages.

4. **Ensure `.nojekyll`**: GitHub Pages may ignore certain files and directories by default, including those starting with underscores. If your documentation includes such directories (common with Doxygen), make sure to include a `.nojekyll` file in your documentation folder to prevent GitHub Pages from ignoring these directories.

5. **Push Changes**: Push the changes to your GitHub repository. This will trigger GitHub Pages to build and deploy your documentation.

6. **Access Documentation**: Once the changes are pushed and GitHub Pages finishes building, your documentation should be accessible at the configured GitHub Pages URL for your repository.

Here's a simple example of how you might configure CMake to generate Doxygen documentation and host it on GitHub Pages:

```cmake
# CMakeLists.txt

cmake_minimum_required(VERSION 3.10)
project(MyProject)

# Locate Doxygen
find_package(Doxygen)

if(DOXYGEN_FOUND)
    # Set input and output directories
    set(DOXYGEN_IN ${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile.in)
    set(DOXYGEN_OUT ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile)

    # Configure the file
    configure_file(${DOXYGEN_IN} ${DOXYGEN_OUT} @ONLY)

    # Add a target to generate Doxygen documentation
    add_custom_target( 
        doc ALL 
        COMMAND ${DOXYGEN_EXECUTABLE} ${DOXYGEN_OUT}
        WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
        COMMENT "Generating API documentation with Doxygen" VERBATIM
    )
else (DOXYGEN_FOUND)
  message("Doxygen needs to be installed to generate the doxygen documentation")
endif (DOXYGEN_FOUND)
```

And here's a sample `Doxyfile.in` which is the input configuration file for Doxygen:

```doxygen
# Doxyfile.in

# Example configuration for Doxygen
INPUT                  = @CMAKE_SOURCE_DIR@
OUTPUT_DIRECTORY       = @CMAKE_BINARY_DIR@/doc
```

Replace `@CMAKE_SOURCE_DIR@` and `@CMAKE_BINARY_DIR@` with appropriate variables. Then, follow the steps outlined above to host the generated documentation on GitHub Pages.

Remember, the specifics may vary depending on your project setup, but this should give you a general idea of how to proceed.

### 1. Code Coverage

Code coverage is a metric used to measure the proportion of source code that is executed during testing. CMake, a cross-platform build system, can be used to generate code coverage reports for projects. Here's a basic overview of how to set up code coverage using CMake:

1. **Compiler Flags**: Enable code coverage flags for your compiler. For example, for GCC and Clang, you can use the `-fprofile-arcs` and `-ftest-coverage` flags.

2. **Instrumentation**: Make sure your code is built with coverage instrumentation. This means compiling your code with the coverage flags mentioned above.

3. **Testing**: Run your tests. Make sure that during testing, the coverage data is generated. This typically involves executing your test suite while the coverage flags are enabled.

4. **Generate Reports**: After running the tests, you need to generate a report from the coverage data. There are tools like `gcov` (for GCC) and `llvm-cov` (for Clang) that can be used for this purpose.

Here's an example of how you might set up CMake to enable code coverage:

```cmake
cmake_minimum_required(VERSION 3.10)
project(MyProject)

# Enable coverage flags for GCC and Clang
if(CMAKE_CXX_COMPILER_ID MATCHES "GNU|Clang")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fprofile-arcs -ftest-coverage")
endif()

# Add your executable or library
add_executable(my_executable source.cpp)

# Add your tests
add_executable(tests test.cpp)

# Link your tests with necessary libraries
target_link_libraries(tests ${CONAN_LIBS})

# Add custom target for running tests
add_custom_target(run_tests COMMAND tests)

# Add custom target for generating coverage report
add_custom_target(coverage
    COMMAND ${CMAKE_COMMAND} -E env "LLVM_PROFILE_FILE=coverage.profraw" ./tests
    COMMAND llvm-profdata merge -sparse coverage.profraw -o coverage.profdata
    COMMAND llvm-cov report -format=html -instr-profile=coverage.profdata $<TARGET_FILE:tests> -o coverage-report
    WORKING_DIRECTORY ${CMAKE_BINARY_DIR}
    DEPENDS tests
)

# Add 'make coverage' target to generate the report
add_custom_target(coverage-report DEPENDS coverage)
```

In this example:

- We enable the coverage flags for GCC and Clang.
- We define a custom target called `coverage`. When you run `make coverage`, it will execute the tests and generate coverage data.
- We use LLVM tools (`llvm-profdata` and `llvm-cov`) to generate a coverage report in HTML format.
- Finally, we define a target `coverage-report` that depends on the `coverage` target, which allows us to simply run `make coverage-report` to generate the coverage report.

Adjust the paths and flags as necessary based on your project structure and compiler.

### 1. Github Actions

To use GitHub Actions with CMake, you can set up a workflow that automatically builds, tests, and possibly deploys your CMake-based project whenever changes are pushed to your repository. Below is a basic example of a GitHub Actions workflow file (`.github/workflows/build.yml`) for a CMake project:

```yaml
name: Build and Test

on:
  push:
    branches:
      - main  # Change this to match your branch name

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up CMake
      uses: lukka/get-cmake@v1
      with:
        cmake-version: '3.21.3'  # You can change this version as needed

    - name: Configure CMake
      run: cmake -B build

    - name: Build
      run: cmake --build build --config Release

    - name: Test
      run: cmake --build build --target test
```

This workflow file specifies the following steps:

1. `Checkout code`: Checks out your repository's code.
2. `Set up CMake`: Installs CMake. In this example, it's using a community action to install CMake, but you can also use pre-installed actions or set up CMake manually if preferred.
3. `Configure CMake`: Configures CMake with the default options. You can customize this step with additional CMake options if needed.
4. `Build`: Builds the project in Release configuration. You can adjust the configuration as needed.
5. `Test`: Runs the tests. You may need to adjust this step based on how your tests are set up.

You can further enhance this workflow to include additional steps such as deploying the built artifacts or running additional tests.

Remember to adjust the workflow according to your project's specific requirements and directory structure. Also, ensure that your CMakeLists.txt file is properly configured to build and test your project.

### 1. Shared vs. Static Library

In CMake, as in many other build systems, you can create either shared or static libraries. Here's an overview of each:

1. **Static Libraries**:
   - Static libraries are archives of object files which are linked directly into your executable at compile time.
   - When you compile your program, the necessary object code from the static library is copied into the final executable.
   - Advantages:
     - Simple deployment: The executable contains all the necessary code, making it easy to distribute.
     - Faster execution: Since all necessary code is already in the executable, there's no need to load additional libraries at runtime.
   - Disadvantages:
     - Larger executables: Each program that uses the static library will contain a copy of the library code, potentially leading to larger executable sizes.
     - No runtime updates: If the library is updated, all programs that use it need to be recompiled to take advantage of the changes.

2. **Shared Libraries**:
   - Shared libraries are separate files that are linked to your executable at either compile time or runtime.
   - When you compile your program, the linker only records a reference to the shared library, and the actual code is loaded into memory when the program is executed.
   - Advantages:
     - Smaller executables: Since the library code is separate, multiple programs can share the same library file, reducing executable size.
     - Runtime updates: If the shared library is updated, all programs using it can take advantage of the changes without needing to be recompiled.
   - Disadvantages:
     - More complex deployment: Shared libraries need to be distributed along with the executable, potentially leading to dependency management issues.
     - Slower startup time: There's overhead in loading shared libraries at runtime, which can result in slightly slower startup times compared to static linking.

In CMake, you can specify whether you want to build a library as shared or static using the `add_library()` function. For example:

```cmake
add_library(mylibrary STATIC ${SOURCE_FILES})  # Static library
add_library(mylibrary SHARED ${SOURCE_FILES}) # Shared library
```

You can also use CMake options to control whether a library should be built as shared or static. For example, you might use `BUILD_SHARED_LIBS` option to toggle between shared and static libraries:

```cmake
set(BUILD_SHARED_LIBS ON)  # Build shared libraries
```

Or:

```cmake
set(BUILD_SHARED_LIBS OFF) # Build static libraries
```

These options can be set either in your CMakeLists.txt file or passed on the command line when invoking CMake.

### 1. Install Command

In CMake, the `install` command is used to specify files and targets to be installed when the `make install` command is executed. This is useful for packaging and distributing software, as it allows you to define what files or targets should be copied to the installation directory.

The syntax of the `install` command is as follows:

```cmake
install(
    [TARGETS targets...]
    [EXPORT export-name]
    [[ARCHIVE|LIBRARY|RUNTIME|INCLUDES|PUBLIC_HEADER|PRIVATE_HEADER|RESOURCE] [DESTINATION <dir>]
    [PERMISSIONS permissions...]
    [CONFIGURATIONS [Debug|Release|...]]
    [COMPONENT <component>]
    [OPTIONAL]
    [EXCLUDE_FROM_ALL]
    [NAMELINK_ONLY]
    [NAMESPACE <namespace>]
    [FILES files...]
    [DIRECTORY dirs...]
    [SCRIPT <file>]
)
```

Here's a brief explanation of some of the commonly used options:

- `TARGETS`: Specifies one or more targets (e.g., executables, libraries) to be installed.
- `EXPORT`: Specifies the name of the export set to use when exporting targets.
- `DESTINATION`: Specifies the directory where the files should be installed.
- `PERMISSIONS`: Specifies the permissions to be set for the installed files.
- `CONFIGURATIONS`: Specifies the build configurations for which the installation should be performed.
- `COMPONENT`: Specifies the installation component. This is useful for grouping related files together.
- `FILES`: Specifies individual files to be installed.
- `DIRECTORY`: Specifies directories whose contents should be installed.
- `SCRIPT`: Specifies a CMake script to be executed during installation.

Here's a simple example of using the `install` command to install a library and headers:

```cmake
# Install library
install(TARGETS my_library
    DESTINATION lib
)

# Install header files
install(FILES my_header.h
    DESTINATION include/my_project
)
```

When you run `make install`, the `my_library` target and `my_header.h` file will be copied to the appropriate installation directories.

### 1. CMake Extension: CMake Cache GUI

As of my last update in January 2022, there wasn't a specific "CMake Cache GUI" extension widely known. However, there are several CMake GUI tools and extensions available that can interact with the CMake cache. Some popular ones include:

1. **CMake GUI**: This is the official graphical user interface for CMake. It allows you to configure CMake projects using a graphical interface, including viewing and modifying CMake cache variables.

2. **CMake Tools for Visual Studio Code**: This extension provides CMake integration directly within Visual Studio Code. While it doesn't have a dedicated "CMake Cache GUI," it allows you to configure and build CMake projects within VS Code, including viewing and modifying CMake cache variables.

3. **cmake-gui**: This is the standalone graphical user interface for CMake. It provides similar functionality to the CMake GUI but can be used independently of any specific IDE.

4. **ccmake**: This is a terminal-based UI for CMake. It's similar to cmake-gui but operates within a terminal environment, making it suitable for remote or headless systems.

These tools generally allow you to view and modify CMake cache variables, which are key to configuring CMake projects. You can use them to adjust build settings, specify paths, enable or disable features, and more, all through a graphical interface or command-line interface. If there have been new developments or specific extensions released since my last update, you may want to check the latest resources and extensions available in the CMake ecosystem.

### 1. CMake Extension: CMake Kits

In the context of CMake, a "CMake Kits" extension could refer to a feature or plugin within an integrated development environment (IDE) or text editor that facilitates the management of CMake projects and their associated build configurations.

CMake is a popular cross-platform build system that allows developers to specify how their software should be built, providing a high level of flexibility and abstraction over the build process. However, configuring CMake projects can sometimes be complex, especially when dealing with different build configurations for different platforms or environments.

A "CMake Kits" extension could streamline this process by providing a user-friendly interface for managing CMake configurations, such as:

1. **Configuration Management**: Allowing users to define different build configurations (or "kits") for their CMake projects, specifying compiler options, target architectures, build types (e.g., debug, release), and other build settings.

2. **Platform Support**: Supporting multiple target platforms (such as Windows, Linux, macOS, or cross-compilation targets) and managing platform-specific build settings within the same project.

3. **Dependency Management**: Simplifying the management of project dependencies, including libraries and external tools required for building the project, by integrating with package managers or providing built-in dependency resolution features.

4. **Build System Integration**: Integrating with popular build systems (such as Make, Ninja, or Visual Studio solutions) to generate build files automatically based on the configured CMake kits.

5. **Project Configuration**: Providing wizards or templates for creating new CMake projects and guiding users through the initial project setup process.

6. **Visualizations and Diagnostics**: Offering visualizations of the project structure, dependency graphs, and build progress, as well as diagnostic tools for troubleshooting build errors and inconsistencies.

7. **Version Control Integration**: Supporting version control systems (such as Git or Subversion) by providing features for managing CMake-related files (such as CMakeLists.txt) and tracking changes to build configurations.

Overall, a "CMake Kits" extension aims to enhance the user experience for CMake developers by simplifying the process of configuring, building, and managing CMake projects across different platforms and environments within their preferred development environment.

### 1. CMake Extension: Debugging and Running

To debug and run CMake projects effectively, you can use various tools and techniques depending on your development environment and preferences. Here's a general guide on how to debug and run CMake projects:

#### 1. Setting Up CMakeLists.txt

Ensure your `CMakeLists.txt` file is configured properly to enable debugging information. This typically involves setting the appropriate compiler flags. For example, for GCC and Clang, you might use:

```cmake
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -g")
```

#### 2. Generating Build Files

Generate build files using CMake. Depending on your preferred build system and IDE, you can generate Makefiles, Visual Studio project files, etc.

```bash
mkdir build
cd build
cmake ..
```

#### 3. Debugging

##### a. Using IDE

If you're using an Integrated Development Environment (IDE) like Visual Studio Code, CLion, or Visual Studio, you can debug directly from within the IDE. Set breakpoints in your code and use the debugging tools provided by the IDE.

##### b. Command Line

For command-line debugging, you can use tools like `gdb` (GNU Debugger) for Linux or `lldb` for macOS. Run your executable with the debugger:

```bash
gdb ./your_executable
```

Or with `lldb`:

```bash
lldb ./your_executable
```

#### 4. Running

##### a. Executing from IDE

Most IDEs provide options to run your executable directly from within the environment. Simply click on the "Run" or "Execute" button.

##### b. Command Line

If you prefer command-line execution, navigate to the directory containing your built executable and run it:

```bash
./your_executable
```

#### 5. Debugging CMake Scripts

To debug CMake scripts themselves, you can use the `message()` command to print information or variables during the CMake configuration process.

```cmake
message(STATUS "Variable Value: ${VARIABLE_NAME}")
```

#### 6. Using CMake Tools Extension (for Visual Studio Code)

If you're using Visual Studio Code, you can install the CMake Tools extension which provides features like IntelliSense, building, debugging, and running directly from the editor.

#### 7. Additional Tips

- Make sure to check for any errors or warnings generated during the CMake configuration and building process.
- Familiarize yourself with the debugging tools provided by your chosen IDE or debugger to efficiently trace and diagnose issues in your code.
- Regularly review and update your `CMakeLists.txt` file to ensure it reflects changes in your project structure or dependencies.

By following these steps, you should be able to effectively debug and run your CMake projects, whether using command-line tools or an Integrated Development Environment.

### Cross Compilation (Toolchains)

Cross-compilation with CMake involves building software for a platform different from the one where the build is executed. This is commonly used when targeting embedded systems, IoT devices, or when developing software for different architectures.

CMake provides support for cross-compilation through toolchain files. A toolchain file tells CMake where to find the cross-compilation tools (compiler, linker, etc.), and sets various parameters such as system libraries, include paths, and compiler flags.

Here's a basic overview of how to use CMake for cross-compilation:

1. **Create a Toolchain File**: This is a script file that specifies the cross-compilation settings. The toolchain file typically sets variables such as `CMAKE_SYSTEM_NAME`, `CMAKE_C_COMPILER`, `CMAKE_CXX_COMPILER`, `CMAKE_FIND_ROOT_PATH`, and any other necessary flags or paths.

2. **Configure Your Project with CMake**: When configuring your project with CMake, specify the toolchain file using the `-DCMAKE_TOOLCHAIN_FILE` option. For example:

   ```bash
   cmake -DCMAKE_TOOLCHAIN_FILE=<path/to/toolchain_file> <path/to/source>
   ```

3. **Build Your Project**: After configuring with CMake, build your project as usual using the generated build system files (e.g., Makefiles, Visual Studio solution).

Here's an example of a simple toolchain file for cross-compiling for ARM Cortex-M microcontrollers with the GNU toolchain:

```cmake
# Specify the cross-compilation settings
SET(CMAKE_SYSTEM_NAME Generic)
SET(CMAKE_SYSTEM_PROCESSOR arm)

# Specify the cross-compilation toolchain
SET(CMAKE_C_COMPILER arm-none-eabi-gcc)
SET(CMAKE_CXX_COMPILER arm-none-eabi-g++)

# Set the root directory for finding libraries and headers
SET(CMAKE_FIND_ROOT_PATH /path/to/cross-compiler/sysroot)

# Set compiler flags and other options if needed
# SET(CMAKE_C_FLAGS ...)
# SET(CMAKE_CXX_FLAGS ...)
```

You would save this script as a file, e.g., `arm_toolchain.cmake`, and then specify it when running CMake as mentioned earlier.

Remember to replace `/path/to/cross-compiler/sysroot` with the appropriate path to your cross-compilation toolchain's sysroot directory, which contains the necessary headers and libraries for the target platform.

By using CMake with a toolchain file, you can streamline the process of cross-compilation and ensure that your project builds correctly for your target platform.

### Using Pre-Compiled Libraries

Using pre-compiled libraries in CMake involves several steps to ensure that the build system can locate and link against these libraries correctly. Here's a general guide on how to do it:

1. **Locate the Pre-Compiled Libraries**: First, make sure you have the pre-compiled libraries available on your system. These can be third-party libraries or libraries that you or your team have compiled earlier.

2. **Set Up the CMakeLists.txt File**:

   a. Use the `find_package()` command to locate the pre-compiled library. This command searches for configuration files provided by the library and sets up variables that you can use in your project.

   ```cmake
   find_package(YourLibrary REQUIRED)
   ```

   Here, `YourLibrary` should be replaced with the name of the library you're using.

3. **Specify Include Directories and Link Libraries**:

   a. After finding the package, you need to specify the include directories for the library headers and link against the library itself. This is usually done using the `target_include_directories()` and `target_link_libraries()` commands.

   ```cmake
   target_include_directories(your_target PRIVATE ${YourLibrary_INCLUDE_DIRS})
   target_link_libraries(your_target PRIVATE ${YourLibrary_LIBRARIES})
   ```

   Replace `your_target` with the name of your target (executable or library).

4. **Complete Example**:

   Here's a complete example of how you might set up your `CMakeLists.txt` file:

   ```cmake
   cmake_minimum_required(VERSION 3.0)
   project(YourProject)

   # Find the pre-compiled library
   find_package(YourLibrary REQUIRED)

   # Add your executable
   add_executable(your_executable main.cpp)

   # Include directories
   target_include_directories(your_executable PRIVATE ${YourLibrary_INCLUDE_DIRS})

   # Link libraries
   target_link_libraries(your_executable PRIVATE ${YourLibrary_LIBRARIES})
   ```

5. **Specify Additional Configuration**:

   Depending on the library, you might need to specify additional configuration options such as version constraints, minimum required version, or specific components of the library to link against. Refer to the documentation of the library for such details.

6. **Build Your Project**:

   After setting up your `CMakeLists.txt` file, you can generate build files using CMake and then build your project using your preferred build system (e.g., Makefiles, Ninja, Visual Studio, etc.).

By following these steps, CMake should be able to find and link against your pre-compiled libraries correctly, allowing you to use them in your project.

### ImGui

ImGui stands for "Dear ImGui" which stands for "Immediate Mode Graphical User Interface". It's a popular, lightweight, and portable GUI library primarily used in video game development and other real-time applications. ImGui allows developers to create user interfaces through immediate mode, where GUI elements are created and manipulated directly within the application's main loop.

Immediate mode GUIs work differently from retained mode GUIs, which are more common in traditional frameworks. In retained mode, you create and manipulate GUI elements which are then drawn by the framework in subsequent frames. In immediate mode, you construct the GUI every frame. This makes immediate mode GUIs more lightweight and suitable for real-time applications where the GUI needs to be tightly integrated with the application logic.

ImGui provides a simple API for creating various GUI elements such as buttons, sliders, text inputs, and more. It's highly customizable and can be easily integrated into existing projects due to its minimal dependencies.

One of the key benefits of ImGui is its ease of use and rapid prototyping capabilities. Developers can quickly create and iterate on GUI layouts without much overhead. Additionally, ImGui is platform-independent and can be used with various rendering backends such as OpenGL, DirectX, Vulkan, and others.

Overall, ImGui is a powerful tool for developers looking to add user interfaces to their applications with minimal hassle and overhead.
