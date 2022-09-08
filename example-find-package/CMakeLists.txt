cmake_minimum_required(VERSION 3.14)
project(phtree-example-find-package)

#include(FetchContent)
#
#FetchContent_Declare(
#        phtree
#        GIT_REPOSITORY https://github.com/tzaeschke/phtree-cpp.git
#        GIT_TAG v1.3.0
#)
#FetchContent_MakeAvailable(phtree)

find_package(phtree CONFIG REQUIRED)

add_executable(ExampleFind example.cc)
target_link_libraries(ExampleFind phtree)
