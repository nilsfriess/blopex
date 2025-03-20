# CMake 2.8.8 introduced an "OBJECT" library type that can be created
# with add_library. An object library compiles source files but does not
# archive or link their object files into a library.
# So we require minimum version 2.8.8.
cmake_minimum_required (VERSION 2.8.8 FATAL_ERROR)

project(MULTIVECTOR C) #'C' indicates that this is a C project

add_library(multivector OBJECT multivector.c)
target_include_directories(multivector OBJECT PUBLIC ${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/../utilities)
add_library(temp_multivector OBJECT temp_multivector.c)
target_include_directories(temp_multivector OBJECT PUBLIC ${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/../utilities)

# Install the header files to the include directory at destination.
# The backslash after ${CMAKE_CURRENT_SOURCE_DIR} copies only the files.
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/
        DESTINATION include
        FILES_MATCHING PATTERN "*.h"
)
