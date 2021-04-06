cmake_minimum_required(VERSION 3.7)

set(NNOM_PROJECT_NAME nnom)

project(${NNOM_PROJECT_NAME})

find_package(Git)
if (GIT_FOUND AND EXISTS "${CMAKE_SOURCE_DIR}/../../.git")
    # Get the latest abbreviated commit hash of the working branch
    execute_process(
            COMMAND ${GIT_EXECUTABLE} rev-parse --short HEAD
            WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
            OUTPUT_VARIABLE PROJECT_VERSION_REVISION
            OUTPUT_STRIP_TRAILING_WHITESPACE
    )
else ()
    message(WARNING "Git not found, cannot set version info")
    SET(PROJECT_VERSION_REVISION "unknown")
endif ()

set(CMAKE_C_STANDARD 99)

if (UNIX AND NOT APPLE)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fPIC")
endif (UNIX AND NOT APPLE)

if (MSVC)
    add_compile_options(/W4)
else ()
    add_compile_options(-Wall -Wextra -Wpedantic -Werror)
endif ()

include_directories(
        inc
        src)

file(GLOB_RECURSE Sources
        "*.h"
        "*.c"
        "*.cpp"
        )

add_library(${NNOM_PROJECT_NAME} ${Sources})

