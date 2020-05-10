cmake_minimum_required(VERSION 2.8.3)
project(lpsolve_catkin)

find_package(catkin_simple REQUIRED)
catkin_simple()

include(ExternalProject)

file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include)

ExternalProject_Add(lpsolve_src
  URL https://github.com/ethz-asl/thirdparty_library_binaries/raw/master/lp_solve_5.5.2.0_source.tar.gz
  UPDATE_COMMAND ""
  CONFIGURE_COMMAND cd ../lpsolve_src && pwd && cp ${PROJECT_SOURCE_DIR}/CMakeLists_lpsolve.txt ../lpsolve_src/CMakeLists.txt && cmake -DCMAKE_INSTALL_PREFIX=${CATKIN_DEVEL_PREFIX} .
  BUILD_COMMAND cd ../lpsolve_src && make -j8
  INSTALL_COMMAND cd ../lpsolve_src && make install -j8 && pwd
)

cs_add_library(${PROJECT_NAME} src/dependency_tracker.cc)
add_dependencies(${PROJECT_NAME} lpsolve_src)
target_link_libraries(${PROJECT_NAME} ${CATKIN_DEVEL_PREFIX}/lib/liblpsolve${CMAKE_SHARED_LIBRARY_SUFFIX})

cs_install()

cs_export(INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/include
  CFG_EXTRAS lpsolve-extras.cmake)
