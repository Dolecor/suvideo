cmake_minimum_required(VERSION 3.14)
project(suvideo C)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c11 -Wall")
set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)

add_subdirectory(3d_party_libs/libav)
add_subdirectory(3d_party_libs/libattopng)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/out)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/out)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/out)

add_library(suvideo SHARED
    src/split.c
    src/unite.c
    src/deleteFrames.c
    )

set_target_properties(suvideo PROPERTIES PUBLIC_HEADER include/suvideo.h)

target_include_directories(suvideo
    PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include
    )

target_link_libraries(suvideo libav libattopng)
