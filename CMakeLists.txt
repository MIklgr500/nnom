cmake_minimum_required(VERSION 3.7)

project(nnom)

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

