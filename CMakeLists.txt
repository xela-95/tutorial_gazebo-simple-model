cmake_minimum_required(VERSION 3.12)

# produce the cmake var PROJECT_NAME
project(tutorial_gazebo-simple-model)

# mandatory use of these packages
find_package(ICUBcontrib REQUIRED)

# extend the current search path used by cmake to load helpers
list(APPEND CMAKE_MODULE_PATH ${ICUBCONTRIB_MODULE_PATH})

# helpers defining certain macros
include(ICUBcontribHelpers)
include(ICUBcontribOptions)

# specify to install in $ICUBcontrib_DIR/bin
icubcontrib_set_default_prefix()

# Install models
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/gazebo/models DESTINATION share/gazebo)

# Install worlds
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/gazebo/worlds DESTINATION share/gazebo)


# generate ad-hoc project to perform "make uninstall"
icubcontrib_add_uninstall_target()
