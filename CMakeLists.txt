cmake_minimum_required(VERSION 3.2)#версия с-make
project(IOT_SCREEN_EMULATOR CXX)

set(CMAKE_CXX_STANDARD 11)

if(CMAKE_COMPILER_IS_GNUCC)
	option(ENABLE_COVERAGE "Enable coverage reporting for gcc/clang" FALSE)
	
	if(ENABLE_COVERAGE)
		add_compile_options(--coverage -O0)
	endif()
endif()

if(MSVC)
	add_compile_options(/W4)
else()
	add_compile_options(-Wall -Wextra -Wpedantic)
endif()

file(GLOB SCREEN_EMULATOR *.cpp *.hpp *.c *.h)

add_library(IOT_SCREEN_EMULATOR ${SCREEN_EMULATOR})

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/glad/)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/glad/include/)

find_package(glfw3 REQUIRED)
find_package(OpenGL REQUIRED)
include_directories(${OpenGL_INCLUDE_DIRS})

target_link_libraries(IOT_SCREEN_EMULATOR ${OPENGL_LIBRARIES} glfw ${GLFW_LIBRARIES} glad --coverage)