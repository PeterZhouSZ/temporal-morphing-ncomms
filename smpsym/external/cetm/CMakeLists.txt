cmake_minimum_required(VERSION 3.6)

set( CMAKE_CXX_STANDARD 14 )

set(EIGEN3_DIR "../eigen")

set( CMAKE_DEBUG_POSTFIX d )

set( CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/lib )
set( CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/lib )

project( cetm )

include_directories(${EIGEN3_DIR})
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

file( GLOB SRCFILES *.cpp )
	
file( GLOB INCFILES *.h include/cetm/*.h)

#set( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11" )
#set( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -openmp" )
	
if (MSVC)
	source_group(TREE ${PROJECT_SOURCE_DIR} PREFIX Source FILES ${SRCFILES})
	source_group(TREE ${PROJECT_SOURCE_DIR} PREFIX Header FILES ${INCFILES})

	set( CMAKE_CXX_FLAGS_DEBUG  "${CMAKE_CXX_FLAGS_DEBUG} -MTd" )
	set( CMAKE_CXX_FLAGS_RELEASE  "${CMAKE_CXX_FLAGS_RELEASE} -MT" )
endif ()

add_library(${PROJECT_NAME} STATIC ${SRCFILES} ${INCFILES})

if ( MSVC )
    set_target_properties( ${PROJECT_NAME} PROPERTIES LIBRARY_OUTPUT_DIRECTORY_DEBUG ${CMAKE_CURRENT_SOURCE_DIR}/lib )
    set_target_properties( ${PROJECT_NAME} PROPERTIES LIBRARY_OUTPUT_DIRECTORY_RELEASE ${CMAKE_CURRENT_SOURCE_DIR}/lib )
    set_target_properties( ${PROJECT_NAME} PROPERTIES ARCHIVE_OUTPUT_DIRECTORY_DEBUG ${CMAKE_CURRENT_SOURCE_DIR}/lib )
    set_target_properties( ${PROJECT_NAME} PROPERTIES ARCHIVE_OUTPUT_DIRECTORY_RELEASE ${CMAKE_CURRENT_SOURCE_DIR}/lib )
endif ( MSVC )