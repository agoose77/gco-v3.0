cmake_minimum_required(VERSION 3.12)

project(gco
        LANGUAGES CXX
        VERSION 0.1
        HOMEPAGE_URL "https://github.com/agoose77/gco"
        DESCRIPTION "GCO")

#
# Make the default build us c++11 and "RELEASE" (-O3)
#
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif(NOT CMAKE_BUILD_TYPE)

include(GNUInstallDirs)

add_library(gco
        SHARED
        src/GCoptimization.cpp
        src/LinkedBlockList.cpp
        )

target_include_directories(gco
        PUBLIC
        # Include directories move depending upon whether building or installing
        $<INSTALL_INTERFACE:include>
        $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
        )

# Install the library, recording the targets
install(TARGETS gco
        EXPORT gco-targets
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
        INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
        )

# Copy headers to destination
install(DIRECTORY include/ DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

# Install the import script for usage by other libraries
install(EXPORT gco-targets
        FILE
        GCOTargets.cmake
        NAMESPACE
        GCO::
        DESTINATION
        ${CMAKE_INSTALL_LIBDIR}/cmake/GCO
        )