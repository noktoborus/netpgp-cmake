# vim: ft=cmake:et:ts=4:ff=unix:fenc=utf-8:
cmake_minimum_required(VERSION 3.0.2)
set(pname mj)

project(${pname} C)

set(build_type SHARED)
if (BUILD_STATIC)
    set(build_type STATIC)
endif ()

add_library(${pname} ${LIBRARY_BUILD_TYPE} mj.c)

set_target_properties(${pname} PROPERTIES PUBLIC_HEADER mj.h)

set(MJ_INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR} PARENT_SCOPE)

install(TARGETS ${pname}
    LIBRARY DESTINATION lib
    PUBLIC_HEADER DESTINATION include
    )

