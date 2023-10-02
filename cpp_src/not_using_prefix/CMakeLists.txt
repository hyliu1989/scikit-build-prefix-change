cmake_minimum_required(VERSION 3.15...3.26)

set(PROJECT_NAME not_using_prefix_example)
project(${PROJECT_NAME} LANGUAGES CXX)
set(lib_name noprefix)

find_package(Python REQUIRED COMPONENTS Interpreter Development.Module)
find_package(pybind11 CONFIG REQUIRED)

set(CMAKE_CXX_STANDARD 17)

file(GLOB SRC src/*.cpp)
pybind11_add_module(${lib_name} ${SRC} empty.cpp)
target_link_libraries(${lib_name} PRIVATE pybind11::headers)
install(
        TARGETS ${lib_name}
        ARCHIVE DESTINATION ${EXAMPLE_RELATIVE_LOCATION}
        LIBRARY DESTINATION ${EXAMPLE_RELATIVE_LOCATION}
        RUNTIME DESTINATION ${EXAMPLE_RELATIVE_LOCATION}
)
