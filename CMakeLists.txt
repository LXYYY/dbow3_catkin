cmake_minimum_required(VERSION 2.8.3)
project(dbow3_catkin)

find_package(catkin_simple REQUIRED)
catkin_simple()

include(ExternalProject)

file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include)

SET(DBOW3_SRC_PATH "dbow3_src")
SET(DBOW3_BUILD_PATH "dbow3_build")
ExternalProject_Add(
  dbow3_src
  GIT_REPOSITORY https://github.com/rmsalinas/DBow3.git
  GIT_TAG c5ae539
  UPDATE_COMMAND ""
  SOURCE_DIR ${DBOW3_SRC_PATH}
  BINARY_DIR ${DBOW3_BUILD_PATH}
  CONFIGURE_COMMAND cd ../${DBOW3_BUILD_PATH} && cmake 
    ../${DBOW3_SRC_PATH} -DCMAKE_INSTALL_PREFIX=${CATKIN_DEVEL_PREFIX}
  BUILD_COMMAND cd ../${DBOW3_BUILD_PATH} && make -j8
  INSTALL_COMMAND cd ../${DBOW3_BUILD_PATH} && make install -j8
)

cs_install()
cs_export(INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/include
          LIBRARIES DBoW3)

