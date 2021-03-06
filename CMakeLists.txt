# Copyright (C) 2010 RobotCub Consortium
# Authors: Andrea del Prete
# CopyPolicy: Released under the terms of the GNU GPL v2.0.

cmake_minimum_required(VERSION 2.8)
set(PROJECTNAME jtsCalibrationGUI)
PROJECT(${PROJECTNAME})

include_directories(${PROJECT_SOURCE_DIR}/include)
include_directories(${YARP_INCLUDE_DIRS})
include_directories(${ICUB_INCLUDE_DIRS})
include_directories(${GTK2_INCLUDE_DIRS})

add_definitions(${GTK2_DEFINITIONS})

# Search for source code.
FILE(GLOB folder_source src/*.cpp)
FILE(GLOB folder_header include/*.h)
SOURCE_GROUP("Source Files" FILES ${folder_source})
SOURCE_GROUP("Header Files" FILES ${folder_header})

#include_directories(${skinDynLib_INCLUDE_DIRS})

ADD_EXECUTABLE(${PROJECTNAME}  ${folder_source} ${folder_header})

target_link_libraries(${PROJECTNAME} 
	${YARP_LIBRARIES} 
#	${GTKPLUS_LINK_FLAGS} 
	${GTK2_LIBRARIES}
	)#skinDynLib )

if(WIN32)
	INSTALL(TARGETS ${PROJECTNAME} RUNTIME DESTINATION bin)
	SET_TARGET_PROPERTIES(${PROJECTNAME}  PROPERTIES COMPILE_FLAGS /wd4996)
else(WIN32)
	INSTALL(TARGETS ${PROJECTNAME} RUNTIME DESTINATION bin)
endif(WIN32)


