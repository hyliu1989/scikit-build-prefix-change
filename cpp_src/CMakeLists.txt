cmake_minimum_required(VERSION 3.10)

project(skbuild_core_install_path_test LANGUAGES CXX)

if (NOT DEFINED EXAMPLE_INSTALLATION)
    set(EXAMPLE_INSTALLATION OFF)
endif ()

add_subdirectory(using_prefix)
add_subdirectory(not_using_prefix)
add_subdirectory(pre_compiled_artifacts)

