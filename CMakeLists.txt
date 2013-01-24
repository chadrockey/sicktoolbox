cmake_minimum_required(VERSION 2.8.3)
project(sicktoolbox)

find_package(catkin REQUIRED)

if(UNIX AND NOT APPLE)
  set(HAVE_LINUX_SERIAL_H 1)
endif()

find_package(GNUPLOT QUIET)
if(GNUPLOT_FOUND)
  set(HAVE_GNUPLOT 1)
endif()

set(SICKTOOLBOX_VERSION 1.1.0)

configure_file(include/SickConfig.hh.in
  ${CATKIN_DEVEL_PREFIX}/include/SickConfig.hh
)

###########
## Build ##
###########

## Specify additional locations of header files
include_directories(
  include
  include/sicklms1xx
  include/sicklms2xx
  ${CATKIN_DEVEL_PREFIX}/include
)

add_subdirectory(src)
add_subdirectory(examples)

###################################################
## Declare things to be passed to other projects ##
###################################################

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES ld lms1xx lms2xx
)

#############
## Install ##
#############

## Mark executable scripts (Python etc.) for installation
## not required for python when using catkin_python_setup()
# install(PROGRAMS
#   scripts/my_python_script
#   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark executables and/or libraries for installation
# install(TARGETS sicktoolbox sicktoolbox_node
#   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark cpp header files for installation
# install(DIRECTORY include/${PROJECT_NAME}/
#   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
#   FILES_MATCHING PATTERN "*.h"
#   PATTERN ".svn" EXCLUDE
# )

## Mark other files for installation (e.g. launch and bag files, etc.)
# install(FILES
#   # myfile1
#   # myfile2
#   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
# )

#############
## Testing ##
#############

## Add gtest based cpp test target and link libraries
# catkin_add_gtest(${PROJECT_NAME}-test test/test_sicktoolbox.cpp)
# if(TARGET ${PROJECT_NAME}-test)
#   target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME})
# endif()

## Add folders to be run by python nosetests
# catkin_add_nosetests(test)
