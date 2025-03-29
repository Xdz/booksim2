cmake_minimum_required(VERSION 3.30)
project(BookSim VERSION 2.0.0)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED True)
set(CMAKE_CXX_COMPILER g++)

file(GLOB COMMON_CXX_FILES
    src/*.cc
    src/*.cpp
)
file(GLOB ALLOCATOR_CXX_FILES
    src/allocators/*.cc
    src/allocators/*.cpp
)
file(GLOB ROUTER_CXX_FILES
    src/routers/*.cc
    src/routers/*.cpp
)
file(GLOB POWER_CXX_FILES
    src/power/*.cc
    src/power/*.cpp
)
file(GLOB ARBITER_CXX_FILES
    src/arbiters/*.cc
    src/arbiters/*.cpp
)
file(GLOB NETWORK_CXX_FILES
    src/networks/*.cc
    src/networks/*.cpp
)
file(GLOB COMMON_PARSE_FILES
    src/*.tab.c
    src/*.yy.c
)

# 定义子模块
add_library(Allocators OBJECT ${ALLOCATOR_CXX_FILES})
add_library(Routers OBJECT ${ROUTER_CXX_FILES})
add_library(Power OBJECT ${POWER_CXX_FILES})
add_library(Arbiters OBJECT ${ARBITER_CXX_FILES})
add_library(Networks OBJECT ${NETWORK_CXX_FILES})
add_library(CommonParseFiles OBJECT ${COMMON_PARSE_FILES})
add_library(Common_CXX_Files OBJECT ${COMMON_CXX_FILES})


# 添加最终可执行文件
add_executable(BookSim
    $<TARGET_OBJECTS:Allocators>
    $<TARGET_OBJECTS:Routers>
    $<TARGET_OBJECTS:Power>
    $<TARGET_OBJECTS:Arbiters>
    $<TARGET_OBJECTS:Networks>
    $<TARGET_OBJECTS:CommonParseFiles>
    $<TARGET_OBJECTS:Common_CXX_Files>
)

# 设置编译选项
add_compile_options(
    -Wall -g -MMD 
)

include_directories(${PROJECT_BINARY_DIR}/src)
include_directories(${PROJECT_BINARY_DIR}/src/allocators)
include_directories(${PROJECT_BINARY_DIR}/src/routers)
include_directories(${PROJECT_BINARY_DIR}/src/power)
include_directories(${PROJECT_BINARY_DIR}/src/arbiters)
include_directories(${PROJECT_BINARY_DIR}/src/networks)



