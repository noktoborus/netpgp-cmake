# vim: ft=cmake:et:ts=4:ff=unix:fenc=utf-8:
cmake_minimum_required(VERSION 3.0.2)

set(pname netpgpkeys)
project(${pname} C)

find_package(OpenSSL)
find_package(BZip2)

include_directories(
    ${MJ_INCLUDE_DIRS}
    ${NETPGP_INCLUDE_DIRS}
    )

add_executable(${pname}
    netpgpkeys.c
    )

target_link_libraries(${pname}
    mj
    netpgp
    ${OPENSSL_CRYPTO_LIBRARY}
    ${BZIP2_LIBRARIES})

