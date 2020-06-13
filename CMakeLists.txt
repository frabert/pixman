cmake_minimum_required(VERSION 3.1)

set(PIXMAN_VERSION_MAJOR 0)
set(PIXMAN_VERSION_MINOR 40)
set(PIXMAN_VERSION_MICRO 1)

project(pixman
        VERSION ${PIXMAN_VERSION_MAJOR}.${PIXMAN_VERSION_MINOR}.${PIXMAN_VERSION_MICRO}
        LANGUAGES C)

add_library(pixman)

configure_file(pixman/pixman-version.h.in pixman-version.h @ONLY)

target_sources(pixman
        PRIVATE
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-access.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-access-accessors.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-bits-image.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-combine32.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-combine-float.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-conical-gradient.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-filter.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-x86.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-mips.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-arm.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-ppc.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-edge.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-edge-accessors.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-fast-path.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-glyph.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-general.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-gradient-walker.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-image.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-implementation.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-linear-gradient.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-matrix.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-noop.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-radial-gradient.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-region16.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-region32.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-solid-fill.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-timer.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-trap.c
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman/pixman-utils.c
)
target_include_directories(pixman
        PRIVATE
                ${CMAKE_CURRENT_SOURCE_DIR}
                ${CMAKE_CURRENT_SOURCE_DIR}/pixman
                ${CMAKE_CURRENT_BINARY_DIR}
)
target_compile_definitions(pixman
        PRIVATE
                PACKAGE=pixman-1
                PACKAGE_VERSION=""
                PACKAGE_BUGREPORT=""
)

if(MSVC)
        if(CMAKE_SIZEOF_VOID_P STREQUAL "8")
                target_compile_definitions(pixman
                        PRIVATE
                                USE_X86_SSE2
                )
        endif()
else()
        if(CMAKE_SIZEOF_VOID_P STREQUAL "8")
                target_compile_definitions(pixman
                        PRIVATE
                                USE_X86_MMX
                                USE_X86_SSE2
                )
        endif()
endif()