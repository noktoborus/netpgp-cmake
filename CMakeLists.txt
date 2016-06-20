# vim: ft=cmake:et:ts=4:ff=unix:fenc=utf-8:
cmake_minimum_required(VERSION 3.0.2)

option(BUILD_STATIC "build as static library" OFF)

if (BUILD_STATIC)
    set(LIBRARY_BUILD_TYPE STATIC)
else ()
    set(LIBRARY_BUILD_TYPE SHARED)
endif ()

add_subdirectory(src/libmj)
add_subdirectory(src/lib)

add_subdirectory(src/netpgp)

