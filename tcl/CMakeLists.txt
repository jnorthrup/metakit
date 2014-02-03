find_package(TCL)

include_directories (../include . ${TCL_INCLUDE_PATH})

set(metakit_tcl_SOURCES mk4tcl.cpp mk4too.cpp)
add_library(Mk4tcl SHARED ${metakit_tcl_SOURCES})
target_link_libraries(Mk4tcl mk4 ${TCL_LIBRARY})
