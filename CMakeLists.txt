cmake_minimum_required(VERSION 3.15)
project(itkpix-efuse-codec)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

set(CMAKE_CXX_STANDARD 17)

if(CMAKE_CXX_COMPILER_ID MATCHES "GNU")
    if(CMAKE_CXX_COMPILER_VERSION VERSION_LESS 7.3)
        message(FATAL_ERROR "GCC version must be at least 7.3")
    endif()
elseif(CMAKE_CXX_COMPILER_ID MATCHES "Clang")
    if(CMAKE_CXX_COMPILER_VERSION VERSION_LESS 6.0)
        message(FATAL_ERROR "Clang version must be at least 6.0")
    endif()
else()
    message(WARNING "Untested compiler \"${CMAKE_CXX_COMPILER_ID}\", proceed with caution!")
endif()

set(ITKPIX_EFUSE_CODEC_INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/src/cpp/)

option(BUILD_PYTHON "Build the python bindings" OFF)

add_subdirectory(exts/hamming-codec)
#add_subdirectory(src)

include_directories(${HAMMING_CODEC_INCLUDE_DIRS})
message(STATUS "Found itkpix-efuse-codec: ITKPIX_EFUSE_CODEC_INCLUDE_DIRS = ${ITKPIX_EFUSE_CODEC_INCLUDE_DIRS}")
