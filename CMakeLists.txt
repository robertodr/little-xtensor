cmake_minimum_required(VERSION 3.1)
project(first_example)

find_package(pybind11 REQUIRED)

find_package(xtensor REQUIRED CONFIG)

find_package(xtensor-python REQUIRED CONFIG)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)
find_package(NumPy REQUIRED)

set(CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS} "-Xclang" "-std=c++14")

pybind11_add_module(first_example MODULE THIN_LTO src/example.cpp)

#if(MSVC)
#  target_compile_options(first_example PRIVATE /EHsc /MP /bigobj /std:c++14)
#  set(CMAKE_EXE_LINKER_FLAGS /MANIFEST:NO)
#else()
#  target_compile_options(first_example PRIVATE -std=c++14)
#endif()

#add_compile_options(
#  "$<$<AND:$<C_COMPILER_ID:Clang>,$<BOOL:${WIN32}>>:-Xclang>"
#  "$<$<AND:$<CXX_COMPILER_ID:Clang>,$<BOOL:${WIN32}>>:-Xclang>"
#  )

target_include_directories(first_example
  PRIVATE
    ${NUMPY_INCLUDE_DIRS}
  )

target_link_libraries(first_example
  PRIVATE
    xtensor-python
  )
