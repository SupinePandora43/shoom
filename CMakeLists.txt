
cmake_minimum_required(VERSION 2.8)

project(shoom)

option(SHOOM_BUILD_TESTS "Build tests for shoom" ON)

include_directories("include")

if (SHOOM_BUILD_TESTS)
    enable_testing()
    add_subdirectory(test)
endif()

set (SOURCE_DIR src)

add_library(shoom STATIC "src/shoom.cpp")

if (${CMAKE_GENERATOR} MATCHES "Visual")
    target_compile_options(shoom PRIVATE -W3 -EHsc)
else()
    target_compile_options(shoom PRIVATE -Wall -Wno-missing-braces -std=c++11 -fPIC)
endif()

if (${CMAKE_SYSTEM_NAME} STREQUAL "Linux")
    target_link_libraries(shoom -lrt) # shm_*
endif() # Linux
