#
# This Source Code Form is subject to the terms of the Mozilla Public
# License, v. 2.0. If a copy of the MPL was not distributed with this
# file, You can obtain one at http://mozilla.org/MPL/2.0/.
#
# Copyright 2024 (c) Aleksander Rozhkov <aleksprog@hotmail.com>
#

cmake_minimum_required(VERSION 3.18)

project(nodesetexporter-demo
        VERSION 1.0.0
        DESCRIPTION "An example of including and using nodesetexporter as a shared library."
        LANGUAGES CXX)

# Installing the C++ Language Standard
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Set compiler flags.
set(CMAKE_CXX_FLAGS_DEBUG_INIT "-Wall -Werror")
set(CMAKE_CXX_FLAGS_RELEASE_INIT "-Wall -Werror")

# Set default build type.
if (NOT CMAKE_BUILD_TYPE)
    message(STATUS "CMAKE_BUILD_TYPE is not set. Set it to 'Release' by default.")
    set(CMAKE_BUILD_TYPE "Release")
endif ()

add_subdirectory(3rdparty)

find_package(open62541 REQUIRED)
find_package(nodesetexporter REQUIRED)

add_library(${PROJECT_NAME}-static STATIC)
target_sources(
        ${PROJECT_NAME}-static
        PUBLIC
        include/apps/nodesetexporter-demo/Application.h
        include/apps/nodesetexporter-demo/BrowseOperations.h
        PRIVATE
        src/apps/nodesetexporter-demo/Application.cpp
        src/apps/nodesetexporter-demo/BrowseOperations.cpp
)

target_include_directories(
        ${PROJECT_NAME}-static
        PUBLIC
        include/
        3rdparty/fmt-10.2.0/include/
)

target_link_libraries(
        ${PROJECT_NAME}-static
        PUBLIC
        nodesetexporter-demo
        nodesetexporter
        open62541::open62541
        fmt::fmt
)

add_executable(${PROJECT_NAME})
target_sources(
        ${PROJECT_NAME}
        PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/src/main.cpp
)

target_link_libraries(
        ${PROJECT_NAME}
        PUBLIC
        ${PROJECT_NAME}-static
)
