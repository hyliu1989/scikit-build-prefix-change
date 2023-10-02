cmake_minimum_required(VERSION 3.18)


# create project
set(PROJECT_NAME using_prefix_example)
project(${PROJECT_NAME} LANGUAGES CXX)
set(lib_name withprefix)

add_library(${lib_name} SHARED)
target_sources(${lib_name} PRIVATE empty2.cpp)
install(
        TARGETS ${lib_name}
        ARCHIVE DESTINATION ${CMAKE_INSTALL_PREFIX}/${EXAMPLE_RELATIVE_LOCATION}/lib
        LIBRARY DESTINATION ${CMAKE_INSTALL_PREFIX}/${EXAMPLE_RELATIVE_LOCATION}/lib
        RUNTIME DESTINATION ${CMAKE_INSTALL_PREFIX}/${EXAMPLE_RELATIVE_LOCATION}/bin
)
