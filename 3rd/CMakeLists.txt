cmake_minimum_required(VERSION 3.5)

project(print)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_INSTALL_RPATH "./")
set(CMAKE_INSTALL_PREFIX "/usr/local/")

message("print your test message")
message(${CMAKE_CURRENT_SOURCE_DIR})

add_library (${PROJECT_NAME} SHARED ${CMAKE_CURRENT_SOURCE_DIR}/src/print.cpp)
    
INSTALL(TARGETS ${PROJECT_NAME} DESTINATION cmake_sample)