cmake_minimum_required(VERSION 3.23)
project(breakout_game)

set(CMAKE_CXX_STANDARD 14)

# Find SFML library
set(SFML_DIR "path/to/SFML/lib/cmake/SFML")
find_package(SFML 2.5 COMPONENTS system window graphics network audio REQUIRED)

# Add executable
add_executable(breakout_game main.cpp background.cpp background.h ball.cpp ball.h constants.h entity.h)

# Link SFML library
target_link_libraries(breakout_game sfml-system sfml-window sfml-graphics sfml-audio sfml-network)

# Copy resources directory to build directory
file(COPY resources DESTINATION ${CMAKE_BINARY_DIR})

# Set resources directory as working directory
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})

# Tell SFML to look for resources in the resources directory
set(SFML_RESOURCES_DIRECTORY "${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/resources")
configure_file(config.hpp.in config.hpp)
target_include_directories(breakout_game PRIVATE ${CMAKE_BINARY_DIR})

include_directories(/usr/local/include)

set(RESOURCE_PATH "${PROJECT_SOURCE_DIR}")

include_directories(${SFML_INCLUDE_DIRS})