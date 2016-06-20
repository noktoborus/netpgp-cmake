# vim: ft=cmake:et:ts=4:ff=unix:fenc=utf-8:
cmake_minimum_required(VERSION 3.0.2)

set(pname netpgp-cli)
project(${pname} C)

find_package(BZip2)
find_package(OpenSSL)

add_executable(${pname} netpgp.c)

target_link_libraries(${pname}
    netpgp
    mj
    ${BZIP2_LIBRARIES}
    ${OPENSSL_CRYPTO_LIBRARY}
    )

set_target_properties(${pname} PROPERTIES OUTPUT_NAME "netpgp")

