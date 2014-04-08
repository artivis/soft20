cmake_minimum_required(VERSION 2.8.3)
project(soft20)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  
)

## System dependencies are found with CMake's conventions
# find_package(Boost REQUIRED COMPONENTS system)


## Uncomment this if the package has a setup.py. This macro ensures
## modules and global scripts declared therein get installed
## See http://ros.org/doc/api/catkin/html/user_guide/setup_dot_py.html
# catkin_python_setup()

################################################
## Declare ROS messages, services and actions ##
################################################

## To declare and build messages, services or actions from within this
## package, follow these steps:
## * Let MSG_DEP_SET be the set of packages whose message types you use in
##   your messages/services/actions (e.g. std_msgs, actionlib_msgs, ...).
## * In the file package.xml:
##   * add a build_depend and a run_depend tag for each package in MSG_DEP_SET
##   * If MSG_DEP_SET isn't empty the following dependencies might have been
##     pulled in transitively but can be declared for certainty nonetheless:
##     * add a build_depend tag for "message_generation"
##     * add a run_depend tag for "message_runtime"
## * In this file (CMakeLists.txt):
##   * add "message_generation" and every package in MSG_DEP_SET to
##     find_package(catkin REQUIRED COMPONENTS ...)
##   * add "message_runtime" and every package in MSG_DEP_SET to
##     catkin_package(CATKIN_DEPENDS ...)
##   * uncomment the add_*_files sections below as needed
##     and list every .msg/.srv/.action file to be processed
##   * uncomment the generate_messages entry below
##   * add every package in MSG_DEP_SET to generate_messages(DEPENDENCIES ...)

## Generate messages in the 'msg' folder
# add_message_files(
#   FILES
#   Message1.msg
#   Message2.msg
# )

## Generate services in the 'srv' folder
# add_service_files(
#   FILES
#   Service1.srv
#   Service2.srv
# )

## Generate actions in the 'action' folder
# add_action_files(
#   FILES
#   Action1.action
#   Action2.action
# )

## Generate added messages and services with any dependencies listed here
# generate_messages(
#   DEPENDENCIES
#   std_msgs  # Or other packages containing msgs
# )

###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## INCLUDE_DIRS: uncomment this if you package contains header files
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES soft20
#  CATKIN_DEPENDS libfftw3
#  DEPENDS system_lib
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
# include_directories(include)
include_directories(
  ${catkin_INCLUDE_DIRS} include
)

## Declare a cpp library

add_library(	soft20-sym

	     	src/lib0/cospmls.c
		src/lib0/FFTcode.c
		src/lib0/fft_grids.c
		src/lib0/fft_grids_so3.c
		src/lib0/FST_semi_memo.c
		src/lib0/indextables.c
		src/lib0/legendreTransforms.c
		src/lib0/newFCT.c
		src/lib0/oddweights.c
		src/lib0/OURmods.c
		src/lib0/OURperms.c
		src/lib0/permroots.c
		src/lib0/rotate_so3.c
		src/lib0/rotate_so3_mem.c
		src/lib0/so3_correlate_sym.c
		src/lib0/soft.c
		src/lib0/soft_sym.c
		src/lib0/weights.c
		src/lib0/wignerTransforms_sym.c
		src/lib0/wrap_s2_rotate.c
		src/lib0/wrap_soft.c
		src/lib0/wrap_soft_sym.c
		src/lib0/wrap_soft_sym_cor2.c
)

add_library(	soft20-fftw

		src/lib1/rotate_so3_fftw.c
		src/lib1/rotate_so3_utils.c
		src/lib1/s2_cospmls.c
		src/lib1/s2_legendreTransforms.c
		src/lib1/s2_semi_fly.c
		src/lib1/s2_semi_memo.c
		src/lib1/so3_correlate_fftw.c
		src/lib1/soft_fftw.c
		src/lib1/soft_fftw_nt.c
		src/lib1/soft_fftw_pc.c
		src/lib1/utils_vec_cx.c
		src/lib1/wignerTransforms_fftw.c
		src/lib1/wrap_s2_rotate_fftw.c
		src/lib1/wrap_soft_fftw.c
		src/lib1/wrap_soft_fftw_cor2.c
)
target_link_libraries(soft20-fftw -lfftw3)

add_library(	soft20-common

		src/common/csecond.c
		src/common/makeweights.c
		src/common/makeWigner.c
		src/common/s2_primitive.c
		src/common/utils_so3.c
		src/common/wignerTransforms.c
)


## Declare a cpp executable

add_executable(test_genWig examples/test_genWig.c)
target_link_libraries(test_genWig soft20-common m)

add_executable(test_Wigner_Analysis examples/test_Wigner_Analysis.c)
target_link_libraries(test_Wigner_Analysis soft20-common m)

add_executable(test_Wigner_angle examples/test_Wigner_angle.c)
target_link_libraries(test_Wigner_angle soft20-common m)

add_executable(test_Wigner_Naive examples/test_Wigner_Naive.c)
target_link_libraries(test_Wigner_Naive soft20-common m)

add_executable(test_Wigner_Synthesis examples/test_Wigner_Synthesis.c)
target_link_libraries(test_Wigner_Synthesis soft20-common m)

add_executable(test_wigSpec examples/test_wigSpec.c)
target_link_libraries(test_wigSpec soft20-common m)



add_executable(test_s2_rotate examples0/test_s2_rotate.c)
target_link_libraries(test_s2_rotate soft20-sym soft20-common m)

add_executable(test_s2_rotate_mem examples0/test_s2_rotate_mem.c)
target_link_libraries(test_s2_rotate_mem soft20-sym soft20-common m)

add_executable(test_s2_rotate_wrap examples0/test_s2_rotate_wrap.c)
target_link_libraries(test_s2_rotate_wrap soft20-sym soft20-common m)

add_executable(test_soft examples0/test_soft.c)
target_link_libraries(test_soft soft20-sym soft20-common m)

add_executable(test_soft_for examples0/test_soft_for.c)
target_link_libraries(test_soft_for soft20-sym soft20-common m)

add_executable(test_soft_inv examples0/test_soft_inv.c)
target_link_libraries(test_soft_inv soft20-sym soft20-common m)

add_executable(test_soft_sym examples0/test_soft_sym.c)
target_link_libraries(test_soft_sym soft20-sym soft20-common m)

add_executable(test_soft_sym_correlate2 examples0/test_soft_sym_correlate2.c)
target_link_libraries(test_soft_sym_correlate2 soft20-sym soft20-common m)

add_executable(test_soft_sym_correlate2_wrap examples0/test_soft_sym_correlate2_wrap.c)
target_link_libraries(test_soft_sym_correlate2_wrap soft20-sym soft20-common m)

add_executable(test_soft_sym_correlate examples0/test_soft_sym_correlate.c)
target_link_libraries(test_soft_sym_correlate soft20-sym soft20-common m)

add_executable(test_soft_sym_for examples0/test_soft_sym_for.c)
target_link_libraries(test_soft_sym_for soft20-sym soft20-common m)

add_executable(test_soft_sym_inv examples0/test_soft_sym_inv.c)
target_link_libraries(test_soft_sym_inv soft20-sym soft20-common m)



add_executable(test_s2_rotate_fftw examples1/test_s2_rotate_fftw.c)
target_link_libraries(test_s2_rotate_fftw soft20-fftw soft20-common m)

add_executable(test_s2_rotate_fftw_mem examples1/test_s2_rotate_fftw_mem.c)
target_link_libraries(test_s2_rotate_fftw_mem soft20-fftw soft20-common m)

add_executable(test_s2_rotate_fftw_wrap examples1/test_s2_rotate_fftw_wrap.c)
target_link_libraries(test_s2_rotate_fftw_wrap soft20-fftw soft20-common m)

add_executable(test_soft_fftw examples1/test_soft_fftw.c)
target_link_libraries(test_soft_fftw soft20-fftw soft20-common m)

add_executable(test_soft_fftw_correlate2 examples1/test_soft_fftw_correlate2.c)
target_link_libraries(test_soft_fftw_correlate2 soft20-fftw soft20-common m)

add_executable(test_soft_fftw_correlate2_wrap examples1/test_soft_fftw_correlate2_wrap.c)
target_link_libraries(test_soft_fftw_correlate2_wrap soft20-fftw soft20-common m)

add_executable(test_soft_fftw_for examples1/test_soft_fftw_for.c)
target_link_libraries(test_soft_fftw_for soft20-fftw soft20-common m)

add_executable(test_soft_fftw_inv examples1/test_soft_fftw_inv.c)
target_link_libraries(test_soft_fftw_inv soft20-fftw soft20-common m)

add_executable(test_soft_fftw_nt examples1/test_soft_fftw_nt.c)
target_link_libraries(test_soft_fftw_nt soft20-fftw soft20-common m)

add_executable(test_soft_fftw_pc examples1/test_soft_fftw_pc.c)
target_link_libraries(test_soft_fftw_pc soft20-fftw soft20-common m)


## Add cmake target dependencies of the executable/library
## as an example, message headers may need to be generated before nodes
# add_dependencies(soft20_node soft20_generate_messages_cpp)

## Specify libraries to link a library or executable target against
# target_link_libraries(soft20_node
#   ${catkin_LIBRARIES}
# )

#############
## Install ##
#############

# all install targets should use catkin DESTINATION variables
# See http://ros.org/doc/api/catkin/html/adv_user_guide/variables.html

## Mark executable scripts (Python etc.) for installation
## in contrast to setup.py, you can choose the destination
# install(PROGRAMS
#   scripts/my_python_script
#   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark executables and/or libraries for installation
# install(TARGETS soft20 soft20_node
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
# catkin_add_gtest(${PROJECT_NAME}-test test/test_soft20.cpp)
# if(TARGET ${PROJECT_NAME}-test)
#   target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME})
# endif()

## Add folders to be run by python nosetests
# catkin_add_nosetests(test)
