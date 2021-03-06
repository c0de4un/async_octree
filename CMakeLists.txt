# // ------------------------------------------------------------------------------ \\
#
# This is CMake-File for OcTree Example Project.
#
# License: see "LICENSE" file.
# API: C++ 11.
# Platforms: Any with C++ 11 support.
#
# // ------------------------------------------------------------------------------ \\

# =================================================================================
# CMake Meta-Data
# =================================================================================

# CMake-Version
cmake_minimum_required ( VERSION 3.8 FATAL_ERROR)

# =================================================================================
# PROJECT
# =================================================================================

# Project Name
set ( ROOT_PROJECT_NAME "octree_example" )

# Configure Project
project ( ${ROOT_PROJECT_NAME} VERSION 1.0 LANGUAGES C CXX )

# =================================================================================
# CONFIG
# =================================================================================

# DETECT LINUX
if ( UNIX AND NOT DEFINED LINUX AND NOT APPLE )
		
	# LINUX ON
	set ( LINUX ON )
	
endif ( UNIX AND NOT DEFINED LINUX AND NOT APPLE )

# PLATFORM
if ( ANDROID ) # ANDROID

	# Set Directory Prefix
	set ( PLATFORM_DIR "android" )
	
elseif ( WIN32 ) # WINDOWS

	# Set Directory Prefix
	set ( PLATFORM_DIR "win32" )

elseif ( LINUX ) # LINUX
	
	# Set Directory Prefix
	set ( PLATFORM_DIR "linux" )

elseif ( APPLE ) # APPLE

	# Set Directory Prefix
	set ( PLATFORM_DIR "apple" )

else ( ANDROID ) # ?
	
	# ERROR
	message ( SEND_ERROR "${ROOT_PROJECT_NAME} - unknown platform ! Configuration required." )
	
	# Set Directory Prefix
	set ( PLATFORM_DIR "unix" )
	
endif ( ANDROID )

# Build-Type Sub-Dir
if ( CMAKE_BUILD_TYPE STREQUAL "Debug" )

	# Add Definition
	add_definitions ( -DDEBUG=1 )
	
	# Set Build-Type Dir
	set ( BUILD_TYPE_DIR "debug" )
	
else ( CMAKE_BUILD_TYPE STREQUAL "Debug" )

	# Set Build-Type Dir
	set ( BUILD_TYPE_DIR "release" )
	
endif ( CMAKE_BUILD_TYPE STREQUAL "Debug" )

# =================================================================================
# CONSTANTS
# =================================================================================

# Set Project Sources Dir
set ( ROOT_PROJECT_SRC_DIR "${CMAKE_SOURCE_DIR}/src/cpp" )

# Set Project Bin-Output Dir
set ( ROOT_PROJECT_OUTPUT_DIR "${CMAKE_SOURCE_DIR}/bin/${BUILD_TYPE_DIR}/${PLATFORM_DIR}" )

# =================================================================================
# HEADERS
# =================================================================================

# Headers
set ( ROOT_PROJECT_HEADERS
"${ROOT_PROJECT_SRC_DIR}/AsyncOctree.hpp" )

# =================================================================================
# SOURCES
# =================================================================================

# Sources
set ( ROOT_PROJECT_SOURCES
"${ROOT_PROJECT_SRC_DIR}/AsyncOctree.cpp"
"${ROOT_PROJECT_SRC_DIR}/main.cpp" )

# =================================================================================
# BUILD EXECUTABLE
# =================================================================================

# Create Executable Object
add_executable ( async_octree_executable ${ROOT_PROJECT_SOURCES} ${ROOT_PROJECT_HEADERS} )

# Configure Executable Object
set_target_properties ( async_octree_executable PROPERTIES
OUTPUT_NAME ${ROOT_PROJECT_NAME}
RUNTIME_OUTPUT_DIRECTORY ${ROOT_PROJECT_OUTPUT_DIR} )