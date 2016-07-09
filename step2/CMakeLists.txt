cmake_minimum_required(VERSION 2.6)
project(Tutorial)

# The version number
set(Tutorial_VERSION_MAJOR 1)
set(Tutorial_VERSION_MINOR 0)

# should we use our own math functions
option(USE_MYMATH "Use tutorial provided math implementation" ON)

# configure a header file to pass some of Cmake settings
# to the source code
configure_file(
    ${PROJECT_SOURCE_DIR}/TutorialConfig.h.in
    ${PROJECT_BINARY_DIR}/TutorialConfig.h
    )

# add the binary tree to the search path for include file 
# so that we wil find TutorialConfig.h 
include_directories(${PROJECT_BINARY_DIR})

# add the MathFunctions library ?
if(USE_MYMATH)
    include_directories(${PROJECT_SOURCE_DIR}/MathFunctions)	# include MathFunctions.h
    add_subdirectory(MathFunctions)             # for creating MathFunction.a file
    set(EXTRA_LIBS ${EXTRA_LIB} MathFunctions)
endif()

# add the executable 
add_executable(Tutorial tutorial.cpp)
target_link_libraries(Tutorial ${EXTRA_LIBS})