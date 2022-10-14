cmake_minimum_required(VERSION 3.23)
project(slava)

set(CMAKE_CXX_STANDARD 17)

file(GLOB INCLUDE_DIRS sourceLibraries)

set(usingDebuggingMode TRUE CACHE BOOL "development mode")

if(usingDebuggingMode)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}  -Wall -Wpedantic -Wextra -Werror")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}  -fsanitize=address,undefined -fno-sanitize-recover=all -fsanitize-undefined-trap-on-error")
endif(usingDebuggingMode)

add_subdirectory(sourceLibraries)

add_executable(${PROJECT_NAME} main.cpp)

target_include_directories(${PROJECT_NAME} PUBLIC ${PRINTER_LIB_INCLUDE_DIRS})
target_link_libraries(${PROJECT_NAME} PRIVATE ${PRINTER_LIB_LIBRARIES})