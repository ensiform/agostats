cmake_minimum_required(VERSION 2.6)

# Project name
set(ProjectName "agostats" CACHE STRING "Project Name")

project(${ProjectName} C)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR})

set(Architecture "x86")

message("Architecture is ${Architecture}")

# Binary names
set(ServerEngine "agostats_server.${Architecture}")
set(ClientEngine "agostats.${Architecture}")

# Paths
set(SrcDir "${CMAKE_SOURCE_DIR}/source")

message("SrcDir is ${SrcDir}")

file(GLOB SOURCE_FILES "${SrcDir}/*.c")
file(GLOB HEADER_FILES "${SrcDir}/*.h")
file(GLOB CSS_FILES "${SrcDir}/*.css")

set(ALL_FILES ${SOURCE_FILES} ${HEADER_FILES} ${CSS_FILES})

source_group("Source Files" FILES ${SOURCE_FILES})
source_group("Header Files" FILES ${HEADER_FILES})
source_group("Style Sheets" FILES ${CSS_FILES})

if(NOT WIN32 AND NOT APPLE)
add_definitions( -DLINUX_STATIC )
endif(NOT WIN32 AND NOT APPLE)

add_executable(${ClientEngine} ${ALL_FILES})

#add_definitions( -DSERVER_STATS )

add_executable(${ServerEngine} ${ALL_FILES})
set_property( TARGET ${ServerEngine} APPEND PROPERTY COMPILE_DEFINITIONS SERVER_STATS )
