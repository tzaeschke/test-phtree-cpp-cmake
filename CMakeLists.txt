cmake_minimum_required(VERSION 3.14)

# set the project name
project(phtree-test-cmake VERSION 1.3.0
        DESCRIPTION "PH-Tree C++ cmake test"
        LANGUAGES CXX)


cmake_policy(SET CMP0077 NEW)

# ---------------------------------------------------------------------------------------
# Set default build to release
# ---------------------------------------------------------------------------------------
if (NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release" CACHE STRING "Choose Release or Debug" FORCE)
endif ()


# ---------------------------------------------------------------------------------------
# Build options
# ---------------------------------------------------------------------------------------
# example options
option(PHT_CMAKE_ALL "Build examples and tests" OFF)

# example options
option(PHT_CMAKE_EXAMPLES "Build examples" ON)
#option(PHT_CMAKE_EXAMPLE_HO "Build header only example" OFF)

# testing options
option(PHT_CMAKE_TESTS "Build tests" OFF)


# ---------------------------------------------------------------------------------------
# Compiler config
# ---------------------------------------------------------------------------------------
find_program(CCACHE_FOUND ccache)
if (CCACHE_FOUND)
    message("CCACHE is found")
    set_property(GLOBAL PROPERTY RULE_LAUNCH_COMPILE ccache)
    set_property(GLOBAL PROPERTY RULE_LAUNCH_LINK ccache)
else (CCACHE_FOUND)
    message("CCACHE is NOT found")
endif (CCACHE_FOUND)

# specify the C++ standard
if (NOT CMAKE_CXX_STANDARD)
    set(CMAKE_CXX_STANDARD 17)
    set(CMAKE_CXX_STANDARD_REQUIRED ON)
endif ()

if (MSVC)
    #set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /std:c++17 /Wall")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /std:c++17")
    set(CMAKE_CXX_FLAGS_RELEASE "/O2")

    if (PHT_CMAKE_TESTS OR PHT_CMAKE_ALL)
        add_compile_options(/bigobj)
    endif ()
else ()
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17 -Wall -Werror")
    set(CMAKE_CXX_FLAGS_RELEASE "-O3 -mavx")
endif ()

# ---------------------------------------------------------------------------------------
# Build binaries
# ---------------------------------------------------------------------------------------
if (PHT_CMAKE_EXAMPLES OR PHT_CMAKE_ALL)
    message(STATUS "Generating examples")
    add_subdirectory(example-fetch)
    #message(STATUS "Generating examples header only")
    #add_subdirectory(example-header-only)
endif ()

if (PHT_CMAKE_TESTS OR PHT_CMAKE_ALL)
    message(STATUS "Generating tests")

    enable_testing()
    include(GoogleTest)
    add_subdirectory(test)
endif ()
