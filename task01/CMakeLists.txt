cmake_minimum_required(VERSION 3.10)  # specify the version of cmake

#############################
# set C++ detail
enable_language(CXX)  # we are using C++
set(CMAKE_CXX_STANDARD 17)  # we are using C++ 17
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)  # we are using STL library
IF(MSVC)
  set(CMAKE_CXX_FLAGS "/W4")
ELSE()
  set(CMAKE_CXX_FLAGS "-Wall -Wextra -g")
ENDIF()

#############################
# set project name

project(task01)

#############################
# specifying libraries to use

# use opengl
find_package(OpenGL REQUIRED)

# use glfw
set(CMAKE_PREFIX_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../external/glfwlib) # give hint to cmake to find glfw library
find_package(glfw3 REQUIRED)

########################
# include, build, and link

include_directories(
    ../external/eigen
)

add_executable(${PROJECT_NAME}
  main.cpp
)

target_link_libraries(${PROJECT_NAME}
  OpenGL::GL  # use OpenGL library
  glfw  # use glfw library
)

#############################
# showing status of libraries
GET_TARGET_PROPERTY(GLFW_INCLUDE_DIR
  glfw INTERFACE_INCLUDE_DIRECTORIES)
message(STATUS "glfw include directory: ${GLFW_INCLUDE_DIR}")