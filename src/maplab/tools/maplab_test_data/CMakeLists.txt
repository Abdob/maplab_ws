cmake_minimum_required (VERSION 2.8)
project(maplab_test_data)

find_package(catkin_simple REQUIRED)
catkin_simple(ALL_DEPS_REQUIRED)

cs_install()

cs_export(CFG_EXTRAS maplab-test-data.cmake maplab-import-test-maps.cmake)
