include_directories(../include)
include_directories(.)

########### next target ###############
set (mk_SRCS
	column.cpp
	column.h
	custom.cpp
	custom.h
	derived.cpp
	derived.h
	fileio.cpp
	field.cpp
	field.h
	format.cpp
	format.h
	handler.cpp
	handler.h
	header.h
	persist.cpp
	persist.h
	remap.cpp
	remap.h
	std.cpp
	std.h
	store.cpp
	store.h
	string.cpp
	table.cpp
  univ.cpp
  univ.h
	view.cpp
	viewx.cpp
)

#MSVC needs static .lib files to work properly
IF(WIN32 OR MSVC)
	add_library(mk SHARED ${mk_SRCS})
else(WIN32 OR MSVC)
	add_library(mk SHARED ${mk_SRCS})
ENDIF(WIN32 OR MSVC)

set_target_properties (mk PROPERTIES VERSION 1.0 SOVERSION 1 INSTALL_RPATH_USE_LINK_PATH on INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/lib")

########### install files ###############

# Targets
install(TARGETS mk DESTINATION lib COMPONENT libraries)
