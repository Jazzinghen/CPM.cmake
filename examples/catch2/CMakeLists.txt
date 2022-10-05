cmake_minimum_required(VERSION 3.14 FATAL_ERROR)

project(CPMExampleCatch2)

# ---- Dependencies ----

include(../../cmake/CPM.cmake)

CPMAddPackage("gh:cpm-cmake/testpack-fibonacci@2.0")
CPMAddPackage("gh:catchorg/Catch2@2.13.4")

# Add Catch2 scripts for automatic test discovery
list(APPEND CMAKE_MODULE_PATH ${Catch2_SOURCE_DIR}/extras)
include(CTest)
include(Catch)

# ---- Create binary ----

add_executable(CPMExampleCatch2 main.cpp)
target_link_libraries(CPMExampleCatch2 fibonacci Catch2)
target_compile_features(CPMExampleCatch2 PRIVATE cxx_std_17)

# ---- Enable testing ----

enable_testing()
catch_discover_tests(CPMExampleCatch2)
