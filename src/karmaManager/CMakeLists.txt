# Copyright: (C) 2012 Department of Robotics Brain and Cognitive Sciences - Istituto Italiano di Tecnologia
# Authors: Vadim Tikhanoff, Ugo Pattacini
# CopyPolicy: Released under the terms of the GNU GPL v2.0.

cmake_minimum_required(VERSION 2.6)
set(PROJECTNAME karmaManager)
project(${PROJECTNAME})
   
find_package(YARP)
find_package(ICUB)
list(APPEND CMAKE_MODULE_PATH ${YARP_MODULE_PATH})
list(APPEND CMAKE_MODULE_PATH ${ICUB_MODULE_PATH})
list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR})

find_package(OpenCV)
find_package(GSL)

find_package(ICUBcontrib)
list(APPEND CMAKE_MODULE_PATH ${ICUBCONTRIB_MODULE_PATH})
include(ICUBcontribHelpers)
include(ICUBcontribOptions)
icubcontrib_set_default_prefix()

include_directories(${PROJECT_SOURCE_DIR}/include
                    ${ctrlLib_INCLUDE_DIRS}
                    ${OpenCV_INCLUDE_DIRS} 
                    ${GSL_INCLUDE_DIRS}
                    ${YARP_INCLUDE_DIRS}
                    )

set(folder_source main.cpp)
# Search for source code.
file( GLOB folder_source src/*.cpp )
file( GLOB folder_header include/iCub/*.h )

source_group("Source Files" FILES ${folder_source})
source_group("Header Files" FILES ${folder_header})

# add executables and link libraries.
add_executable(${PROJECTNAME} ${folder_header} ${folder_source})
target_link_libraries(${PROJECTNAME} ${OpenCV_LIBRARIES} ${GSL_LIBRARIES} ${YARP_LIBRARIES})
install(TARGETS ${PROJECTNAME} DESTINATION bin)

