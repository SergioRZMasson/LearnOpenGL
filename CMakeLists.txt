cmake_minimum_required(VERSION 3.5.0)
project(LearnOpenGL VERSION 0.1.0 LANGUAGES C CXX)

set(LEARN_OPENGL_SOURCES 
    "src/main.cpp"
    "src/colors.hpp"
    "src/ltc_matrix.hpp")

set(LEARN_OPENGL_HEADERS 
    "include/learnopengl/model.h"
    "include/learnopengl/camera.h"
    "include/learnopengl/mesh.h"
    "include/learnopengl/shader.h")

set(LEARN_OPENGL_SHADERS
    "shaders/7.area_light.fs"
    "shaders/7.area_light.vs"
    "shaders/7.light_plane.fs"
    "shaders/7.light_plane.vs")

add_executable(LearnOpenGL ${LEARN_OPENGL_SOURCES} ${LEARN_OPENGL_HEADERS} ${LEARN_OPENGL_SHADERS})

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

target_include_directories(LearnOpenGL PRIVATE src)
target_include_directories(LearnOpenGL PUBLIC include)

# this is heuristically generated, and may not be correct
find_package(glad CONFIG REQUIRED)
target_link_libraries(LearnOpenGL PRIVATE glad::glad)

# this is heuristically generated, and may not be correct
find_package(glfw3 CONFIG REQUIRED)
target_link_libraries(LearnOpenGL PRIVATE glfw)

find_package(glm CONFIG REQUIRED)
target_link_libraries(LearnOpenGL PRIVATE glm::glm)

find_package(assimp CONFIG REQUIRED)
target_link_libraries(LearnOpenGL PRIVATE assimp::assimp)

find_package(Stb REQUIRED)
target_include_directories(LearnOpenGL PRIVATE ${Stb_INCLUDE_DIR})

set_property(DIRECTORY ${CMAKE_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT LearnOpenGL)

