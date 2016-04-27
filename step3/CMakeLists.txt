cmake_minimum_required(VERSION 2.6)
project(Tutorial)

# The version number
set(Tutorial_VERSION_MAJOR 1)
set(Tutorial_VERSION_MINOR 0)

# should we use our own math functions 
option(USE_MYMATH "Use tutorial provided math implementation" ON)

# configure a header file to pass some of the Cmake settings
configure_file(
    ${PROJECT_SOURCE_DIR}/TutorialConfig.h.in 
    ${PROJECT_BINARY_DIR}/TutorialConfig.h
)

# add the binary tree to the search path for include files 
# so that we wil find TutorialConfig.h 
include_directories(${PROJECT_BINARY_DIR})

# add the MathFunctions library ?
if(USE_MYMATH)
    include_directories(${PROJECT_SOURCE_DIR}/MathFunctions)
    add_subdirectory(MathFunctions)
    set(EXTRA_LIBS ${EXTRA_LIBS} MathFunctions)
endif()

# add the executable 
add_executable(Tutorial tutorial.cpp)
target_link_libraries(Tutorial ${EXTRA_LIBS})

# add the install targets 
install(TARGETS Tutorial DESTINATION bin)
install(FILES ${PROJECT_BINARY_DIR}/TutorialConfig.h DESTINATION include)

# enable testing 
enable_testing()

# define a macro to simplify adding tests, then use it 
macro(do_test arg result)
    add_test(TutorialComp${arg} Tutorial ${arg})
    set_tests_properties(TutorialComp${arg} PROPERTIES PASS_REGULAR_EXPRESSION ${result})
endmacro(do_test)

# does the application run 
add_test(TutorialRuns Tutorial 25)

# does it sqrt of 25
#add_test(TutorialComp25 Tutorial 25)
#set_tests_properties(TutorialComp25 PROPERTIES PASS_REGULAR_EXPRESSION "25 is 5")
do_test(25 "25 is 5")  # 25 is input and 5 is output
do_test(4 "4 is 2")