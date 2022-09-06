cmake_minimum_required(VERSION 3.14)
project(phtree-tests LANGUAGES CXX)

include(FetchContent)
include(scripts.cmake)

FetchContent_Declare(
        googletest
        GIT_REPOSITORY https://github.com/google/googletest.git
        GIT_TAG release-1.12.1
)
if (MSVC)
    # Avoids LNK2038 Error with MSVC
    set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
endif ()
FetchContent_MakeAvailable(googletest)

# The next line is optional, but keeps your CACHE cleaner:
mark_as_advanced(
        BUILD_GMOCK BUILD_GTEST BUILD_SHARED_LIBS
        gmock_build_tests gtest_build_samples gtest_build_tests
        gtest_disable_pthreads gtest_force_shared_crt gtest_hide_internal_symbols
)

# If you are interested in keeping IDEs that support folders clean, I would also add these lines:
set_target_properties(gtest PROPERTIES FOLDER extern)
set_target_properties(gtest_main PROPERTIES FOLDER extern)

package_add_test(phtree_test phtree_test.cc)
