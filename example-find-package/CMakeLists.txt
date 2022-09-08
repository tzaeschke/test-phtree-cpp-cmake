cmake_minimum_required(VERSION 3.14)
project(phtree-example-find-package)

find_package(phtree CONFIG REQUIRED PATHS ${CMAKE_SOURCE_DIR}/my_packages)
#find_package(phtree CONFIG REQUIRED)

add_executable(ExampleFind example.cc)
target_link_libraries(ExampleFind phtree::phtree)
