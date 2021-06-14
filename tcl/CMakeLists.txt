include  (FindTclStub)
option (USE_TCL_STUBS "Enable use of TCL stubs library")

include (FindPkgConfig)
ADD_DEFINITIONS("-std=c++11")

include  (FindTclStub)
if (USE_TCL_STUBS)
ADD_DEFINITIONS("-DUSE_TCL_STUBS")
endif (USE_TCL_STUBS)

set (CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_SOURCE_DIR})

include_directories(${TCL_INCLUDE_PATH})
include_directories(../include)

include_directories(.)

set (Mk4tcl_SRCS
	../src/custom.cpp
	../src/column.cpp
	../src/derived.cpp
	../src/field.cpp
	../src/fileio.cpp
	../src/format.cpp
	../src/handler.cpp
	../src/persist.cpp
	../src/remap.cpp
	../src/std.cpp
	../src/store.cpp
	../src/string.cpp
	../src/table.cpp
	../src/univ.cpp
	../src/view.cpp
	../src/viewx.cpp
	mk4tcl.cpp
	mk4tcl.h
	mk4too.cpp
)

add_library(Mk4tcl SHARED ${Mk4tcl_SRCS})

if (USE_TCL_STUBS)
	target_link_libraries(Mk4tcl ${TCL_STUB_LIBRARY})
else (USE_TCL_STUBS)
	target_link_libraries(Mk4tcl ${TCL_LIBRARY})
endif (USE_TCL_STUBS)

set_target_properties (Mk4tcl PROPERTIES VERSION 0.1 SOVERSION 0 PREFIX "" INSTALL_RPATH_USE_LINK_PATH on INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/lib/${PACKAGE}")

install(TARGETS Mk4tcl DESTINATION lib/${PACKAGE})

install(FILES
	pkgIndex.tcl
	DESTINATION lib/${PACKAGE})
