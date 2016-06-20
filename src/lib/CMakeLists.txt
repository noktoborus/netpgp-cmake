# vim: ft=cmake:et:ts=4:ff=unix:fenc=utf-8:
cmake_minimum_required(VERSION 3.0.2)

set(pname "netpgp")
project(${pname} C)

include(CheckIncludeFiles)
include(CheckTypeSize)

find_package(BZip2)
find_package(OpenSSL)

include_directories(
    ${CMAKE_CURRENT_BINARY_DIR}
    ${MJ_INCLUDE_DIRS}
    ${BZIP2_INCLUDE_DIRS}
    ${OPENSSL_INCLUDE_DIR})

set(PACKAGE_VERSION "20140220")
set(PACKAGE_BUGREPORT "Alistair Crooks <agc@netbsd.org> c0596823")
check_include_files(bzlib.h HAVE_BZLIB_H)
check_include_files(commoncrypto/commondigests.h
    HAVE_COMMONCRYPTO_COMMONDIGEST_H)
check_include_files(direct.h HAVE_DIRECT_H)
check_include_files(dlfcn.h HAVE_DLFCN_H)
check_include_files(dmalloc.h HAVE_DMALLOC_H)
check_include_files(errno.h HAVE_ERRNO_H)
check_include_files(fcntl.h HAVE_FCNTL_H)
check_include_files(inttypes.h HAVE_INTTYPES_H)
check_include_files(limits.h HAVE_LIMITS_H)
check_type_size("long long int" HAVE_LONG_LONG_INT LANGUAGE "C")
check_include_files(malloc.h HAVE_MALLOC_H)
check_include_files(memory.h HAVE_MEMORY_H)

if (OPENSSL_FOUND)
    check_include_files(openssl/aes.h HAVE_OPENSSL_AES_H)
    check_include_files(openssl/bn.h HAVE_OPENSSL_BN_H)
    check_include_files(openssl/camellia.h HAVE_OPENSSL_CAMELLIA_H)
    check_include_files(openssl/cast.h HAVE_OPENSSL_CAST_H)
    check_include_files(openssl/des.h HAVE_OPENSSL_DES_H)
    check_include_files(openssl/dsa.h HAVE_OPENSSL_DSA_H)
    check_include_files(openssl/err.h HAVE_OPENSSL_ERR_H)
    check_include_files(openssl/idea.h HAVE_OPENSSL_IDEA_H)
    check_include_files(openssl/md5.h HAVE_OPENSSL_MD5_H)
    check_include_files(openssl/rand.h HAVE_OPENSSL_RAND_H)
    check_include_files(openssl/rsa.h HAVE_OPENSSL_RSA_H)
    check_include_files(openssl/sha.h HAVE_OPENSSL_SHA_H)
    if (HAVE_OPENSSL_SHA_H)
        set(CMAKE_EXTRA_INCLUDE_FILES "openssl/sha.h")
        check_type_size(SHA256_CTX HAVE_SHA256_CTX LANGUAGE "C")
        set(CMAKE_EXTRA_INCLUDE_FILES)
    endif ()
endif()

check_include_files(stdint.h HAVE_STDINT_H)
check_include_files(stdlib.h HAVE_STDLIB_H)
check_include_files(strings.h HAVE_STRINGS_H)
check_include_files(sys/cdefs.h HAVE_SYS_CDEFS_H)
check_include_files(sys/file.h HAVE_SYS_FILE_H)
check_include_files(sys/mman.h HAVE_SYS_MMAN_H)
check_include_files(sys/param.h HAVE_SYS_PARAM_H)
check_include_files(sys/resource.h HAVE_SYS_RESOURCE_H)
check_include_files(sys/stat.h HAVE_SYS_STAT_H)
check_include_files(sys/types.h HAVE_SYS_TYPES_H)
check_include_files(sys/uio.h HAVE_SYS_UIO_H)
check_include_files(unistd.h HAVE_UNISTD_H)
check_type_size("unsigned long long int" HAVE_UNSIGNED_LONG_LONG_INT
    LANGUAGE "C")
check_include_files(zlib.h HAVE_ZLIB_H)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/config.h.in
    ${CMAKE_CURRENT_BINARY_DIR}/config.h)

add_library(${pname} ${LIBRARY_BUILD_TYPE}
    symmetric.c
    packet-parse.c
    signature.c
    misc.c
    packet-print.c
    netpgp.c
    ssh2pgp.c
    validate.c
    create.c
    openssl_crypto.c
    keyring.c
    bufgap.c
    packet-show.c
    reader.c
    crypto.c
    compress.c
    writer.c
    )

add_dependencies(${pname} mj)

set(NETPGP_INCLUDE_DIRS ${CMAKE_CURRENT_BINARY_DIR} PARENT_SCOPE)

