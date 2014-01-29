set(PYTHON_VERSION_MAJOR 2)
find_package(PythonLibs 2)

include_directories (../include . ./scxx ${PYTHON_INCLUDE_DIRS})

set(metakit_python_SOURCES 
    PyProperty.cpp
    PyRowRef.cpp
    PyStorage.cpp
    PyView.cpp
    scxx/PWOImp.cpp)
add_library(Mk4py SHARED ${metakit_python_SOURCES})
target_link_libraries(Mk4py mk4 ${PYTHON_LIBRARIES})

