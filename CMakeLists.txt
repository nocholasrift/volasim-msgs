cmake_minimum_required(VERSION 3.16)
project(volasim_msgs LANGUAGES CXX)

find_package(protobuf CONFIG REQUIRED)

set(PROTO_FILES
  msg/Header.proto
  msg/Thrust.proto
  msg/Imu.proto
  msg/Odometry.proto
  msg/DroneState.proto
  msg/DepthCamera.proto
  msg/Transform.proto
  msg/Trajectory.proto
)

set(PROTO_OUT_DIR ${CMAKE_CURRENT_BINARY_DIR}/volasim_msgs)
file(MAKE_DIRECTORY ${PROTO_OUT_DIR})

add_library(volasim_msgs STATIC ${PROTO_FILES})
target_include_directories(volasim_msgs PUBLIC ${CMAKE_CURRENT_BINARY_DIR})
set_target_properties(volasim_msgs PROPERTIES CXX_STANDARD 17 CXX_STANDARD_REQUIRED ON)
target_link_libraries(volasim_msgs PUBLIC protobuf::libprotobuf)

protobuf_generate(
  TARGET volasim_msgs
  LANGUAGE cpp
  IMPORT_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/msg
  PROTOC_OUT_DIR ${PROTO_OUT_DIR}
)
