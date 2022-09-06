cmake_minimum_required(VERSION 3.14)
project(phtree-example-fetch-content)

 # Example executable that uses FetchContent

include(FetchContent)

FetchContent_Declare(
        phtree
        GIT_REPOSITORY https://github.com/tzaeschke/phtree-cpp.git
        #GIT_TAG v1.3.0
        GIT_TAG 7f6c6157fcc9be75b8cf333016d4db93f29b7855
)
FetchContent_MakeAvailable(phtree)

add_executable(ExampleFetch example.cc)
target_link_libraries(ExampleFetch phtree)
