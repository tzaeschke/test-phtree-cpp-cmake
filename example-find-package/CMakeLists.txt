cmake_minimum_required(VERSION 3.14)
project(phtree-example-header-only)

include(FetchContent)
#include(common/scripts.cmake)

FetchContent_Declare(
        phtree
        GIT_REPOSITORY https://github.com/tzaeschke/phtree-cpp.git
        GIT_TAG v1.3.0
)
FetchContent_MakeAvailable(phtree)

if (WIN32 OR UNIX)
    add_executable(ExampleFind example.cc)
    target_include_directories(ExampleFind INTERFACE phtree) #${PROJECT_SOURCE_DIR}/include/..)
else ()
    add_executable(ExampleFind example.cc)
    target_link_libraries(ExampleFind phtree)
endif ()