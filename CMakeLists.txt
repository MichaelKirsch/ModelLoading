cmake_minimum_required(VERSION 3.15)

set(CMAKE_CXX_STANDARD 17 )
set(PROJECT_NAME MK_ENGINE_2)
project(${PROJECT_NAME})
link_libraries(stdc++fs) #link the filesystem

set(GLFW_DIR "${CMAKE_CURRENT_LIST_DIR}/libs/glfw-3.3.1")
set(SFML_DIR "${CMAKE_CURRENT_LIST_DIR}/libs/SFML-2.5.1/lib/cmake/SFML")
file(GLOB_RECURSE SOURCES "src/*.cpp" "src/*.hpp") #glob all the source files intp one place
file(GLOB_RECURSE REQUIRED_DLLS_FOR_SFML "libs/SFML-2.5.1/bin/*.dll" "libs/required_dll/*.dll") #glob all the source files intp one place
file(COPY ${REQUIRED_DLLS_FOR_SFML} DESTINATION ${CMAKE_CURRENT_BINARY_DIR})


add_subdirectory(${GLFW_DIR})
find_package(SFML 2.5.1 COMPONENTS system window graphics network audio REQUIRED)

find_package(OpenGL REQUIRED)

add_executable(${PROJECT_NAME} ${SOURCES} main.cpp libs/glad/src/glad.c  libs/FastNoise/FastNoise.cpp)


target_link_libraries(${PROJECT_NAME} sfml-audio sfml-graphics sfml-window sfml-system glfw ${GLFW_LIBRARIES} ${OPENGL_LIBRARIES} )
