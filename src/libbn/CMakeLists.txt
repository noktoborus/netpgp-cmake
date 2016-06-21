# vim: ft=cmake:et:ts=4:ff=unix:fenc=utf-8:
cmake_minimum_required(VERSION 3.0.2)

set(pname bn)
project(${pname} C)

include_directories(${DIGEST_INCLUDE_DIRS})

add_library(${pname} ${LIBRARY_BUILD_TYPE}
    bignum.c
    misc.c
    rand.c
    stubs.c
    )

set(BN_INCLUDE_DIRS "${CMAKE_CURRENT_SOURCE_DIR}" PARENT_SCOPE)

