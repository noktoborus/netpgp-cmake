# vim: ft=cmake:et:ts=4:ff=unix:fenc=utf-8:
cmake_minimum_required(VERSION 3.0.2)

set(pname verify)
project(${pname} C)

add_library(${pname} ${LIBRARY_BUILD_TYPE}
    b64.c
    dump.c
    libverify.c
    pgpsum.c
    )

