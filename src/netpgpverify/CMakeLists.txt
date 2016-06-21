# vim: ft=cmake:et:ts=4:ff=unix:fenc=utf-8:
cmake_minimum_required(VERSION 3.0.2)

set(pname netpgpverify)
project(${pname} C)

add_executable(${pname}
    main.c
    verify.c
    )

