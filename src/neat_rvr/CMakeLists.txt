#
# Set minimum required version
#
cmake_minimum_required(VERSION 2.8)

project(neat_rvr)
##ros part

find_package(catkin REQUIRED COMPONENTS
  roscpp
  tf
  std_msgs
  geometry_msgs
  nav_msgs
  message_generation
)

generate_messages(
  DEPENDENCIES
  std_msgs
  geometry_msgs
  nav_msgs
)

catkin_package(
  LIBRARIES template_controller
  CATKIN_DEPENDS message_runtime roscpp std_msgs geometry_msgs nav_msgs tf
  DEPENDS system_lib
)


include_directories(
  ${catkin_INCLUDE_DIRS}
)

link_libraries(${catkin_LIBRARIES})

#
# Set the path additional cmake files must be searched for
#
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_SOURCE_DIR}/src/cmake)

#
# Make sure we are under Unix
#
if(NOT UNIX)
  message(FATAL_ERROR "ARGoS compiles only under UNIX, sorry!")
endif(NOT UNIX)

#
# Set build options
#
include(${CMAKE_SOURCE_DIR}/cmake/ARGoSBuildOptions.cmake)

#
# Set compiler flags
#
include(${CMAKE_SOURCE_DIR}/cmake/ARGoSBuildFlags.cmake)

#
# Check for libraries
#
include(${CMAKE_SOURCE_DIR}/cmake/ARGoSBuildChecks.cmake)

#
# Set up CPack for later use
#
include(${CMAKE_SOURCE_DIR}/cmake/ARGoSPackaging.cmake)


include(${CMAKE_SOURCE_DIR}/cmake/FindPthreads.cmake)


#
# Compile stuff
#
add_subdirectory(src)
