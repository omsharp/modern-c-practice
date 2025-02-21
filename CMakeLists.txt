cmake_minimum_required(VERSION 3.25.0)

# C standard
set(CMAKE_C_STANDARD 17)

# project name (main executable file name)
project(program)

# determine OS bitness
if(CMAKE_SIZEOF_VOID_P EQUAL 8)
    set(OSBitness 64)
else()
    set(OSBitness 32)
endif()

# build output directory based on OS and build type.
# (example: bin/Linux_64/Debug)
set(FullOutputDir "${CMAKE_SOURCE_DIR}/bin/${CMAKE_SYSTEM_NAME}_${OSBitness}/${CMAKE_BUILD_TYPE}")

# path of the executables
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${FullOutputDir}")

# path of the static libraries. (will be embedded in executable)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${FullOutputDir}/static libs")

# path of the dynamic libraries. (to be shipped with executable)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${FullOutputDir}")

# set the include (headers) directory
include_directories(./include)

# set the source code files
add_executable(${PROJECT_NAME}
    src/main.c)

# add a shared (dynamic) libaray
# add_library("[_myLibraryName]" SHARED [source path])

# add a static library
# add_library("[_myLibraryName]" STATIC [source path])

# link a library to the project
# target_link_libraries(${PROJECT_NAME} "[_libraryName]")

# compiler flags
target_compile_options(program PRIVATE
    -Wall
    -Wextra
    -Wpedantic)