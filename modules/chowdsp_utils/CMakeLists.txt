cmake_minimum_required(VERSION 3.15)
project(chowdsp_utils VERSION 1.0.0)
set(CMAKE_CXX_STANDARD 17)
include(CTest)

option(CHOWDSP_ENABLE_TESTING "Enable testing for chowdsp modules" OFF)
option(CHOWDSP_ENABLE_BENCHMARKS "Enable benchmarks for chowdsp modules" OFF)
option(CHOWDSP_ENABLE_EXAMPLES "Enable examples for chowdsp modules" OFF)

if(NOT (CHOWDSP_ENABLE_TESTING OR CHOWDSP_ENABLE_BENCHMARKS OR CHOWDSP_ENABLE_EXAMPLES))
    # Add CMake utils
    list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)
    include(AddDiagnosticInfo)
    include(SubprojectVersion)

    # Add modules here...
    include(AddJUCEModules)
else()
    list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)
    list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake/test)

    if(CHOWDSP_ENABLE_TESTING)
        add_subdirectory(tests)
    elseif(CHOWDSP_ENABLE_BENCHMARKS)
        add_subdirectory(bench)
    elseif(CHOWDSP_ENABLE_EXAMPLES)
        add_subdirectory(examples)
    endif()
endif()
