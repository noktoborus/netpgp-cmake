# vim: ft=cmake:et:ts=4:ff=unix:fenc=utf-8:
cmake_minimum_required(VERSION 3.0.2)

set(pname digest)
project(${pname} C)

add_library(${pname} ${LIBRARY_BUILD_TYPE}
    tiger.c
    digest.c)

set(DIGEST_INCLUDE_DIRS "${CMAKE_CURRENT_SOURCE_DIR}" PARENT_SCOPE)

