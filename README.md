![Bazel Linux build](https://github.com/tzaeschke/test-phtree-cpp-cmake/actions/workflows/bazel.yml/badge.svg)

# test-phtree-cpp-cmake

This is a test project to verify / demonstrate how to include [phtree-cpp](https://github.com/tzaeschke/phtree-cpp) when using the cmake build system.

This project tests three variations of dependency management with cmake.

1) `add_subdirectory()`: This requires copying the source phtree code into a subfolder. This can be enabled with `PHT_CMAKE_SUB_SIRECTORY`.

2) `FetchContent`: This can be enabled with `PHT_CMAKE_FETCH_CONTENT`

3) `find_package()`: This requirees the phtree being installed on the local system. This can be enabled with `PHT_CMAKE_FIND_PACKAGE`
