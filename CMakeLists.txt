project(gco)
cmake_minimum_required(VERSION 2.8)

if (NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE "Release")
endif()

set(lib_srcs
    src/GCoptimization.cpp
    src/LinkedBlockList.cpp
    )


add_library(gco ${lib_srcs})
target_include_directories(gco
    PUBLIC
    ${CMAKE_SOURCE_DIR}/include
)

install(TARGETS gco
        ARCHIVE DESTINATION "${CMAKE_INSTALL_PREFIX}/lib"
        LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib"
        COMPONENT library)
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
        DESTINATION "${CMAKE_INSTALL_PREFIX}/include"
        FILES_MATCHING PATTERN "*.h" PATTERN "*.inl")

