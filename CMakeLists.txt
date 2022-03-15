cmake_minimum_required(VERSION 3.5)

project(sample)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_INSTALL_RPATH "./")



set(CMAKE_INSTALL_PREFIX ${CMAKE_CURRENT_SOURCE_DIR}/bin)
set(CMAKE_INSTALL_RPATH ${CMAKE_CURRENT_SOURCE_DIR}/3rd/lib)


message("print your test message")
message(${CMAKE_INSTALL_PREFIX})

find_library(PRINT_LIB print ${CMAKE_CURRENT_SOURCE_DIR}/3rd/lib)

#link_directories(${CMAKE_CURRENT_SOURCE_DIR}/3rd/lib)

add_executable(${PROJECT_NAME}
        ${CMAKE_CURRENT_SOURCE_DIR}/src/main.cpp
        )       

target_include_directories(${PROJECT_NAME}
        PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/3rd/src
        )
             


target_link_libraries(${PROJECT_NAME} ${PRINT_LIB})

INSTALL(TARGETS ${PROJECT_NAME} DESTINATION ${CMAKE_INSTALL_PREFIX})