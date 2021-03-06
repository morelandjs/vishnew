cmake_minimum_required(VERSION 2.6)
project(vishnew Fortran)

# default build type: Release
if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE "Release")
endif()

# default install prefix: ~/.local
if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
  set(CMAKE_INSTALL_PREFIX "$ENV{HOME}/.local"
      CACHE PATH "Install path prefix, prepended onto install directories."
      FORCE)
endif()

message(STATUS "Build type: ${CMAKE_BUILD_TYPE}")
message(STATUS "Install prefix: ${CMAKE_INSTALL_PREFIX}")

# Set default architecture flags to optimize for the current system,
# but don't override user settings.
if(NOT CMAKE_Fortran_FLAGS MATCHES "-march|-mtune")
  set(CMAKE_Fortran_FLAGS "${CMAKE_Fortran_FLAGS} -march=native")
endif()

set(CMAKE_Fortran_FLAGS "${CMAKE_Fortran_FLAGS} -cpp")

option(WARNINGS "enable compiler warnings" OFF)
if(WARNINGS)
  set(CMAKE_Fortran_FLAGS "${CMAKE_Fortran_FLAGS} -Wall -Wextra")
endif()

install(FILES ${PROJECT_NAME}.conf DESTINATION share/${PROJECT_NAME})

add_subdirectory(eos)
add_subdirectory(src)
