cmake_minimum_required(VERSION 2.8)

project(fiducial_pose)

find_package(catkin REQUIRED COMPONENTS
  sensor_msgs
  std_msgs
  geometry_msgs
  roscpp
  tf
  fiducial_msgs
)

find_package(OpenCV REQUIRED)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES rpp_pose
)


include_directories(include ${OpenCV_INCLUDE_DIRS})
include_directories(${catkin_INCLUDE_DIRS})


add_library(rpp_pose src/Rpoly.cpp src/RPP.cpp src/calcPose.cpp)
add_dependencies(rpp_pose ${${PROJECT_NAME}_EXPORTED_TARGETS}
                 ${catkin_EXPORTED_TARGETS})

install(TARGETS rpp_pose
   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  PATTERN ".svn" EXCLUDE
)
