cmake_minimum_required(VERSION 3.16)
project(headless-example)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# headless
set(SRC_DIR src)
set(GEN_SRC_DIR gsrc)
set(HEADLESS_COMMAND headless -iglw --from=${SRC_DIR} --to=${GEN_SRC_DIR})
execute_process(COMMAND ${HEADLESS_COMMAND} WORKING_DIRECTORY ${CMAKE_SOURCE_DIR})
add_custom_target(headless COMMAND ${HEADLESS_COMMAND} WORKING_DIRECTORY ${CMAKE_SOURCE_DIR})
include(${GEN_SRC_DIR}/sources.cmake)

add_executable(headless-example ${SOURCES})
add_dependencies(headless-example headless)
