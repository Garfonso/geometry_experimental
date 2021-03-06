cmake_minimum_required(VERSION 2.8.3)
project(tf2_geometry_msgs)

find_package(orocos_kdl)
find_package(catkin REQUIRED COMPONENTS geometry_msgs tf2_ros tf2)
find_package(Boost COMPONENTS thread REQUIRED)

catkin_package(
   INCLUDE_DIRS include
   DEPENDS orocos_kdl 
   CATKIN_DEPENDS  geometry_msgs tf2_ros tf2)


include_directories(include 
                    ${catkin_INCLUDE_DIRS}   
)

link_directories(${orocos_kdl_LIBRARY_DIRS})



install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)

catkin_python_setup()

if(CATKIN_ENABLE_TESTING)

find_package(catkin REQUIRED COMPONENTS geometry_msgs rostest tf2_ros tf2)

add_executable(test_geometry_msgs EXCLUDE_FROM_ALL test/test_tf2_geometry_msgs.cpp)
target_link_libraries(test_geometry_msgs ${catkin_LIBRARIES} ${GTEST_LIBRARIES} ${orocos_kdl_LIBRARIES})
add_rostest(${CMAKE_CURRENT_SOURCE_DIR}/test/test.launch)


if(TARGET tests)
  add_dependencies(tests test_geometry_msgs)
endif()


endif()
