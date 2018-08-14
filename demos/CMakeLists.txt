include_directories(../include ../src .)

add_executable(demo demo.cpp)
target_link_libraries(demo mk4_static)
install(TARGETS demo
	RUNTIME DESTINATION demos)

add_executable(dump dump.cpp)
target_link_libraries(dump mk4_static)
install(TARGETS dump
	RUNTIME DESTINATION demos)

add_executable(myio myio.cpp)
target_link_libraries(myio mk4_static)
install(TARGETS myio
	RUNTIME DESTINATION demos)

