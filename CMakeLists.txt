cmake_minimum_required(VERSION 3.5)

project(sample)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_INSTALL_RPATH "./")

message("print your test message")
message(${CMAKE_CURRENT_SOURCE_DIR})

add_executable(${PROJECT_NAME}
        ${CMAKE_CURRENT_SOURCE_DIR}/src/main.cpp
        )       

target_include_directories(${PROJECT_NAME}
        PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}
        )
        
link_directories(${CMAKE_CURRENT_SOURCE_DIR}/../3rd/grpc/lib)

target_link_libraries(${PROJECT_NAME}
        Print
        rt
        glog
        ${CMAKE_CURRENT_SOURCE_DIR}/../3rd/boringssl/libssl.so
        ${CMAKE_CURRENT_SOURCE_DIR}/../3rd/boringssl/libcrypto.so
        ${CMAKE_CURRENT_SOURCE_DIR}/../3rd/grpc/lib/libprotobuf.so
        ${CMAKE_CURRENT_SOURCE_DIR}/../3rd/grpc/cpp_lib/libgrpc++.so
        ${CMAKE_CURRENT_SOURCE_DIR}/../3rd/libevent/libevent_pthreads.so 
        ${CMAKE_CURRENT_SOURCE_DIR}/../3rd/libevent/libevent_core.so
        ${CMAKE_CURRENT_SOURCE_DIR}/../3rd/libevent/libevent_extra.so
    
        )

INSTALL(TARGETS ${PROJECT_NAME} DESTINATION ${CMAKE_INSTALL_PREFIX})
INSTALL(FILES ${CMAKE_CURRENT_SOURCE_DIR}/config/capability.conf DESTINATION ${CMAKE_INSTALL_PREFIX})
INSTALL(FILES ${CMAKE_CURRENT_SOURCE_DIR}/config/local.conf DESTINATION ${CMAKE_INSTALL_PREFIX})
INSTALL(PROGRAMS ${CMAKE_CURRENT_SOURCE_DIR}/script/start.sh DESTINATION ${CMAKE_INSTALL_PREFIX})
INSTALL(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/../3rd/grpc/lib DESTINATION ${CMAKE_INSTALL_PREFIX}/lib/grpc/)
INSTALL(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/../3rd/grpc/cpp_lib DESTINATION ${CMAKE_INSTALL_PREFIX}/lib/grpc/)
INSTALL(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/../3rd/libevent DESTINATION ${CMAKE_INSTALL_PREFIX}/lib)