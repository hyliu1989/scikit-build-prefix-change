cmake_minimum_required(VERSION 3.21)  # IMPORTED_RUNTIME_ARTIFACTS exists only after 3.21.

project(test_imported LANGUAGES CXX)

set(libname ${CMAKE_CURRENT_LIST_DIR}/binary/libsomeprecompiled.so)

if (TARGET test_imported)
    message(STATUS "test_imported already imported")
else ()
    message(STATUS "Importing test_imported")
    add_library(test_imported SHARED IMPORTED GLOBAL)
    set_target_properties(test_imported PROPERTIES INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_CURRENT_LIST_DIR}/include)
    set_target_properties(test_imported PROPERTIES IMPORTED_LOCATION ${libname})
    if (DEFINED EXAMPLE_INSTALLATION AND EXAMPLE_INSTALLATION)
        # Installing using pre-compiled .so file.
        # install(IMPORTED_RUNTIME_ARTIFACTS test_imported DESTINATION ${EXAMPLE_RELATIVE_LOCATION})
        install(FILES ${libname} DESTINATION ${EXAMPLE_RELATIVE_LOCATION})
    endif ()
endif ()
