cmake_minimum_required(VERSION "3.5.0")

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake/modules")


set(VALID_BUILD_TYPES "Release" "Debug" "MinSizeRel" "RelWithDebInfo")


project("Example")

#set default build type
if(NOT CMAKE_CONFIGURATION_TYPES)
        if(CMAKE_BUILD_TYPE STREQUAL "")
                set(CMAKE_BUILD_TYPE "Release" CACHE STRING "Select build type [${VALID_BUILD_TYPES}]" FORCE)
        endif()
endif()

#set dropdown list in cmake gui
if(NOT CMAKE_CONFIGURATION_TYPES)
        set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS ${VALID_BUILD_TYPES})
endif()

#Make sure the build type is valid
if(NOT CMAKE_CONFIGURATION_TYPES)
        list(FIND VALID_BUILD_TYPES "${CMAKE_BUILD_TYPE}" INDEX)
        if(${INDEX} MATCHES -1)
                message(FATAL_ERROR "Invalid build type <${CMAKE_BUILD_TYPE}>. Valid types are [${VALID_BUILD_TYPES}]")
        endif()
endif()

add_subdirectory("project")

# uninstall target
if(NOT TARGET uninstall)
  configure_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/cmake/cmake_uninstall.cmake.in"
    "${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake"
    IMMEDIATE @ONLY)

  add_custom_target(uninstall
    COMMAND ${CMAKE_COMMAND} -P ${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake)
endif()

# Add cpack 
include("CPackConfig")
include("CPack")
