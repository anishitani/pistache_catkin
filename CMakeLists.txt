cmake_minimum_required(VERSION 3.1)
project(pistache_catkin)

find_package( catkin REQUIRED )

file( MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include )

include( ExternalProject )
ExternalProject_Add(
    project_pistache
    GIT_REPOSITORY https://github.com/oktal/pistache.git
    INSTALL_DIR ${CATKIN_DEVEL_PREFIX}
    CMAKE_ARGS -DBUILD_SHARED_LIBS=ON -DCMAKE_INSTALL_PREFIX=<INSTALL_DIR> )

add_library( ${PROJECT_NAME} SHARED IMPORTED )
set_property( TARGET ${PROJECT_NAME} PROPERTY IMPORTED_LOCATION ${CATKIN_DEVEL_PREFIX}/lib/libpistache${CMAKE_SHARED_LIBRARY_SUFFIX} )
add_dependencies( ${PROJECT_NAME} project_pistache )

catkin_package(
    INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/include
    LIBRARIES ${PROJECT_NAME} )
