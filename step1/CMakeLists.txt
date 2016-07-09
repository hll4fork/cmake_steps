cmake_minimum_required(VERSION 2.8)
project(tutorial)

# The version number.
set (Tutorial_VERSION_MAJOR 1)
set (Tutorial_VERSION_MINOR 0)

# configure a file to pass some of the Cmake settings to the source file
configure_file(
    ${PROJECT_SOURCE_DIR}/TutorialConfig.h.in
    ${PROJECT_BINARY_DIR}/TutorialConfig.h
)

# include generator head file --> TutorialConfig.h
include_directories(${PROJECT_BINARY_DIR})

add_executable(Tutorial tutorial.cpp)