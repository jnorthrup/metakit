set (PACKAGE mk4tcl)
project (${PACKAGE})
cmake_minimum_required (VERSION 3.10)

option (BUILD_SHARED_LIBS "Build Shared Libraries." ON)

# Set up some variables that we can use in our code.
set (VERSION 1.0)
add_definitions (-DHAVE_CONFIG_H)
include_directories (${CMAKE_CURRENT_BINARY_DIR})

include (CheckTypeSize)
CHECK_TYPE_SIZE("long" SIZEOF_LONG)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/config.h.cmake ${CMAKE_CURRENT_BINARY_DIR}/config.h)

# Fix for static library linking to shared library on 64 bit systems:
# with -fPIC
IF(UNIX AND NOT WIN32)
  FIND_PROGRAM(CMAKE_UNAME uname /bin /usr/bin /usr/local/bin )
  IF(CMAKE_UNAME)
    EXEC_PROGRAM(uname ARGS -m OUTPUT_VARIABLE CMAKE_SYSTEM_PROCESSOR)
    SET(CMAKE_SYSTEM_PROCESSOR ${CMAKE_SYSTEM_PROCESSOR} CACHE INTERNAL
			"processor type (i386 and x86_64)")
		 IF(CMAKE_SYSTEM_PROCESSOR MATCHES "x86_64")
		   ADD_DEFINITIONS(-fPIC)
		 ENDIF(CMAKE_SYSTEM_PROCESSOR MATCHES "x86_64")
  ENDIF(CMAKE_UNAME)
ENDIF(UNIX AND NOT WIN32)

add_subdirectory(src)
add_subdirectory(tcl)

# the following lines are needed to build debian/ubuntu packages.
set (CPACK_DEBIAN_PACKAGE_NAME ${PACKAGE})
set (CPACK_DEBIAN_PACKAGE_VERSION ${VERSION})
set (CPACK_DEBIAN_PACKAGE_ARCHITECTURE amd64)
set (CPACK_DEBIAN_PACKAGE_DEPENDS "tcl8.6 (>=8.6.5)")
set (CPACK_DEBIAN_PACKAGE_MAINTAINER "Sam Bromley <sam@sambromley.com>")
set (CPACK_DEBIAN_PACKAGE_DESCRIPTION "Metakit for Tcl")
set (CPACK_DEBIAN_PACKAGE_SECTION "devel")
set (CPACK_DEBIAN_PACKAGE_PRIORITY "optional")
set (DEBIAN_PACKAGE_BUILDS_DEPENDS "tcl8.6-dev (>=8.6.5)")
set (CPACK_GENERATOR "DEB")
set (CPACK_PACKAGE_INSTALL_DIRECTORY "${CMAKE_PATH_PREFIX}/${PACKAGE}/")
set (CPACK_COMPONENTS_ALL libraries headers executables)
set (CPACK_SET_DESTDIR TRUE)
include(CPack)
