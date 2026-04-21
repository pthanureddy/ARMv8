cmake_minimum_required(VERSION 3.20)
project(armv8_pipeline_simulator VERSION 0.1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

option(ARMSIM_BUILD_TESTS "Build GoogleTest unit tests" ON)

add_library(armsim
    src/parser.cpp
    src/simulator.cpp
    src/trace.cpp
)
target_include_directories(armsim PUBLIC include)
target_compile_features(armsim PUBLIC cxx_std_20)

add_executable(armv8_sim src/main.cpp)
target_link_libraries(armv8_sim PRIVATE armsim)

if(ARMSIM_BUILD_TESTS)
  include(FetchContent)
  FetchContent_Declare(
    googletest
    URL https://github.com/google/googletest/archive/refs/tags/v1.15.2.zip
    DOWNLOAD_EXTRACT_TIMESTAMP TRUE
  )
  set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
  FetchContent_MakeAvailable(googletest)

  enable_testing()
  include(GoogleTest)

  add_executable(armsim_tests
      tests/test_decoder.cpp
      tests/test_simulator.cpp
  )
  target_link_libraries(armsim_tests PRIVATE armsim GTest::gtest_main)
  gtest_discover_tests(armsim_tests)
endif()
