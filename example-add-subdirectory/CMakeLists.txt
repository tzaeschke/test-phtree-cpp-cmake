cmake_minimum_required(VERSION 3.14)
project(phtree-example-add-subdirectory)

add_executable(ExampleAddSub example.cc)
add_subdirectory(phtree-cpp)
target_link_libraries(ExampleAddSub phtree)
