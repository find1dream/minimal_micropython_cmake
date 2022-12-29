cmake_minimum_required(VERSION 3.14)

set(MICROPY_DIR            ${CMAKE_CURRENT_LIST_DIR}/micropython)
set(MICROPY_BUILD_RST_DIR  ${CMAKE_CURRENT_LIST_DIR}/build)
set(MICROPY_TARGET         micropython)

include(${MICROPY_DIR}/py/py.cmake)

project(${MICROPY_TARGET})

set(MICROPY_SOURCE_QSTR 
    ${MICROPY_SOURCE_PY}
    ${CMAKE_CURRENT_LIST_DIR}/main.c
    ${CMAKE_CURRENT_LIST_DIR}/mphalport.c
    ${MICROPY_DIR}/shared/libc/printf.c
    ${MICROPY_DIR}/shared/readline/readline.c
    ${MICROPY_DIR}/shared/runtime/pyexec.c
    ${MICROPY_DIR}/shared/runtime/stdout_helpers.c
)

add_executable(${MICROPY_TARGET} 
    ${MICROPY_SOURCE_QSTR}
)

target_include_directories(${MICROPY_TARGET}
    PUBLIC
    ${CMAKE_CURRENT_LIST_DIR}
    ${MICROPY_BUILD_RST_DIR}
    ${MICROPY_DIR}
    )

include(${MICROPY_DIR}/py/mkrules.cmake)
