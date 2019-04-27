cmake_minimum_required(VERSION 3.13)
project(VulkanPlayground)

set(CMAKE_CXX_STANDARD 17)

find_package(Vulkan REQUIRED)
find_package(glm REQUIRED)
find_package(glfw3 REQUIRED)

add_executable(VulkanPlayground main.cpp)

target_link_libraries(VulkanPlayground vulkan glfw glm)