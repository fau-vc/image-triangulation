CMAKE_MINIMUM_REQUIRED(VERSION 2.8.0)

PROJECT(imagetri CXX C)

SET (CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_SOURCE_DIR}/cmake)

FIND_PACKAGE(Eigen3 REQUIRED)
FIND_PACKAGE(AntTweakBar REQUIRED)
FIND_PACKAGE(DirectX REQUIRED)
FIND_PACKAGE(Matlab REQUIRED)

SET(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR})
SET(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR})

IF(WIN32)
  ADD_DEFINITIONS(-DNOMINMAX)
  #ADD_DEFINITIONS(-DWIN32_LEAN_AND_MEAN)
  #ADD_DEFINITIONS(-D_USE_MATH_DEFINES)
  #ADD_DEFINITIONS(-DNODEFAULTLIB)
  #ADD_DEFINITIONS(-DNOGDI)
  #ADD_DEFINITIONS(-D_VARIADIC_MAX=10)  
ENDIF()

FIND_PACKAGE(OpenMP)
IF(OPENMP_FOUND)
  MESSAGE(STATUS "Using OpenMP parallelization")
  SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
  SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
  SET(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_EXE_LINKER_FLAGS}")
ELSE()
  MESSAGE(STATUS "Not using OpenMP parallelization")
ENDIF()

INCLUDE_DIRECTORIES(${CMAKE_HOME_DIRECTORY})

ADD_SUBDIRECTORY(demo)
ADD_SUBDIRECTORY(effect-framework)