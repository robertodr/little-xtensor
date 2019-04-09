cmake_minimum_required(VERSION 3.1)
project(first_example)

find_package(pybind11 REQUIRED)
set(PYBIND11_INCLUDE_DIR ${pybind11_INCLUDE_DIRS})

find_package(xtensor REQUIRED CONFIG)
set(XTENSOR_INCLUDE_DIR ${xtensor_INCLUDE_DIRS})

find_package(xtensor-python REQUIRED CONFIG)
set(XTENSOR_PYTHON_INCLUDE_DIR ${xtensor-python_INCLUDE_DIRS})

add_executable(first_example src/example.cpp)

if(MSVC)
  target_compile_options(first_example PRIVATE /EHsc /MP /bigobj)
  set(CMAKE_EXE_LINKER_FLAGS /MANIFEST:NO)
endif()

if(CMAKE_CXX_COMPILER_ID MATCHES "Clang" OR
   CMAKE_CXX_COMPILER_ID MATCHES "GNU" OR
   (CMAKE_CXX_COMPILER_ID MATCHES "Intel" AND NOT WIN32))
  target_compile_options(first_example PRIVATE -march=native -std=c++14)
endif()

target_link_libraries(first_example xtensor-python)
