cmake_minimum_required(VERSION 3.0.2)
project(go2_hardware_interface)

# Find catkin macros and libraries
find_package(catkin REQUIRED COMPONENTS
  controller_manager
  realtime_tools
  base_hardware_interface
)
      
add_subdirectory(go2_hal)

catkin_package(
 CATKIN_DEPENDS
   controller_manager
   realtime_tools
   base_hardware_interface
)

##########
# Build ##
##########

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)

add_executable(ros_control_node
    src/go2_robot_hw.cpp
    src/go2_ros_control.cpp
    src/go2_ros_node.cpp)

# Specify libraries to link a library or executable target against
target_link_libraries(ros_control_node
  ${catkin_LIBRARIES}
  go2hal
)



set_property(TARGET ros_control_node PROPERTY CXX_STANDARD 11)  # At least std c++11

#############
## Install ##
#############

install(
  TARGETS ros_control_node  test_go2_hal
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

