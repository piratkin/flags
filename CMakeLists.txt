cmake_minimum_required(VERSION 3.0)

set(DEFAULT_PROJECT_NAME ${CMAKE_PROJECT_NAME})
set(DEFAULT_PROJECT_VERSION ${CMAKE_PROJECT_VERSION})

project(flags VERSION 0.0.1 LANGUAGES CXX)

configure_file(flags.h.in flags.h)

add_library(${PROJECT_NAME} INTERFACE)

target_include_directories(${PROJECT_NAME} 
    INTERFACE ${CMAKE_CURRENT_BINARY_DIR})
