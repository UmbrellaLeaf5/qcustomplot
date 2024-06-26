cmake_minimum_required(VERSION 3.14)
project(qcustomplotroot LANGUAGES CXX)

# Find architecture property
if(CMAKE_SIZEOF_VOID_P EQUAL 8)
  set(PROJECT_ARCH_TARGET "amd64") # x64
elseif(CMAKE_SIZEOF_VOID_P EQUAL 4)
  set(PROJECT_ARCH_TARGET "i386") # x86
else()
  message(FATAL_ERROR "Unkwnown architecture, CMake will exit.")
endif()

# Defines options of project
# Ex : set(EXT_OPT_QCPLIB_XYZ 0)

# Export generated binaries
if(NOT PROJECT_BUILD_OUTPUT)
  set(PROJECT_BUILD_OUTPUT ${CMAKE_SOURCE_DIR}/build/output/${PROJECT_ARCH_TARGET}/${CMAKE_BUILD_TYPE})

  SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_BUILD_OUTPUT})
  SET(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_BUILD_OUTPUT})
  SET(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BUILD_OUTPUT})
  SET(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BUILD_OUTPUT})
endif()

# Set project properties
set(PROJECT_NAME qcustomplot)
set(PROJECT_VERSION_SEMANTIC 2.1.1.1)
set(PROJECT_VERSION_CPP_MIN 11)

# Set project options
# Options availables for external project start with "EXT_OPT_QCPLIB_", those options can be use in top CMakeFiles.
# All options are disabled by default.
# List of available options :
# - Currently no options available

# Check for target architecture
if(NOT PROJECT_ARCH_TARGET)
  message(FATAL_ERROR "Cmake variable \"PROJECT_ARCH_TARGET\" is undefined, please set it in your root CMakelist.")
endif()

# Set project configuration
project(${PROJECT_NAME} LANGUAGES CXX)
project(${PROJECT_NAME} VERSION "${PROJECT_VERSION_SEMANTIC}")

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOUIC ON) # Specific to Qt
set(CMAKE_AUTOMOC ON) # Specific to Qt
set(CMAKE_AUTORCC ON) # Specific to Qt

# Set C++ standard to use
if(DEFINED CMAKE_CXX_STANDARD)
  if(${CMAKE_CXX_STANDARD} LESS ${PROJECT_VERSION_CPP_MIN})
    message(FATAL_ERROR "Project ${PROJECT_NAME} require at least C++ standard ${PROJECT_VERSION_CPP_MIN}")
  endif()
else()
  set(CMAKE_CXX_STANDARD ${PROJECT_VERSION_CPP_MIN})
endif()

set(CMAKE_CXX_STANDARD_REQUIRED ON)
message(STATUS "Project \"${PROJECT_NAME}\" compiled with C++ standard ${CMAKE_CXX_STANDARD}")

# Configure file project - File containing macro that can be used in project
configure_file("${CMAKE_CURRENT_SOURCE_DIR}/config.h.in" "${CMAKE_CURRENT_SOURCE_DIR}/config.h")

# Find Qt packages
find_package(QT NAMES Qt6 Qt5 COMPONENTS Core REQUIRED)
find_package(QT NAMES Qt6 Qt5 COMPONENTS PrintSupport REQUIRED)

find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Core REQUIRED)
find_package(Qt${QT_VERSION_MAJOR} COMPONENTS PrintSupport REQUIRED)

# Manage library files
set(PROJECT_HEADERS
  config.h

  qcustomplot.h
)

set(PROJECT_SOURCES
  qcustomplot.cpp
)

set(PROJECT_FILES ${PROJECT_HEADERS} ${PROJECT_SOURCES} ${PROJECT_UI} ${PROJECT_RSC})

# Add files to the library
add_library(${PROJECT_NAME} SHARED ${PROJECT_FILES})

# Set version of library
set_target_properties(${PROJECT_NAME} PROPERTIES
  VERSION ${PROJECT_VERSION}
  SOVERSION ${PROJECT_VERSION_MAJOR})

# Link needed libraries
# Qt Library
target_link_libraries(${PROJECT_NAME} PUBLIC Qt${QT_VERSION_MAJOR}::Core)
target_link_libraries(${PROJECT_NAME} PUBLIC Qt${QT_VERSION_MAJOR}::PrintSupport)

# Compile needed definitions
target_compile_definitions(${PROJECT_NAME} PRIVATE QCUSTOMPLOT_COMPILE_LIBRARY)

# Directories to includes
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
