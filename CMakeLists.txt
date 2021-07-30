cmake_minimum_required(VERSION 2.8.3)
project(pose_graph_tools)

find_package(catkin REQUIRED
    COMPONENTS
    roscpp
    message_runtime
    std_msgs
    geometry_msgs
    visualization_msgs
    interactive_markers
    message_generation
    
)

include_directories(
    include/pose_graph_tools
    include
    ${catkin_INCLUDE_DIRS}
    ${Boost_INCLUDE_DIRS}
    
)
add_compile_options(-std=c++11)

add_message_files(DIRECTORY msg 
    FILES 
      PoseGraph.msg 
      PoseGraphEdge.msg
      PoseGraphNode.msg)

generate_messages(DEPENDENCIES std_msgs geometry_msgs visualization_msgs)

add_library(${PROJECT_NAME}
  src/visualizer.cpp
  ${catkin_LIBRARIES}
)

add_executable(visualizer_node
  src/visualizer_node.cpp
  src/visualizer.cpp
)
target_link_libraries(visualizer_node ${catkin_LIBRARIES})

