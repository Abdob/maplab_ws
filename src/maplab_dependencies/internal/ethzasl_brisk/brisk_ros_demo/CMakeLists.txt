cmake_minimum_required(VERSION 2.4.6)
project(brisk_ros_demo)

find_package(catkin_simple REQUIRED)
catkin_simple(ALL_DEPS_REQUIRED)

if(CMAKE_SYSTEM_PROCESSOR MATCHES "^(aarch64.*|AARCH64.*|arm64.*|ARM64.*)")
	add_definitions(" -DHAVE_OPENCV")
	add_definitions(-msse2 -march=native -Wextra -Wall
                -Wno-overloaded-virtual -Wno-non-virtual-dtor # OpenCV.
                -std=c++0x -DENABLE_BRISK_TIMING -DTEST_IN_SOURCE
                -DHAVE_OPENCV)
else()
	add_definitions(-msse2 -mssse3 -Wextra -Wall
                -Wno-overloaded-virtual -Wno-non-virtual-dtor # OpenCV.
                -std=c++0x -DENABLE_BRISK_TIMING -DTEST_IN_SOURCE
                -DHAVE_OPENCV)
endif()

	#if (NOT (CMAKE_CXX_COMPILER_ID MATCHES "Clang"))
	#add_definitions( -Werror )
	#endif()

cs_add_executable(livedemo src/livedemo.cc)
target_link_libraries(livedemo ${catkin_LIBRARIES})
