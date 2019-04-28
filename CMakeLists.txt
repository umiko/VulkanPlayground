cmake_minimum_required(VERSION 3.13)
project(VulkanPlayground)

set(CMAKE_CXX_STANDARD 17)

find_package(Vulkan REQUIRED)

if (UNIX)
    find_package(glm REQUIRED)
    find_package(glfw3 REQUIRED)
endif ()

if(WIN32)
    include_directories($ENV{glm_DIR}/glm)
    add_subdirectory($ENV{glfw_DIR} cmake-build-debug/glfw)
endif()

add_executable(VulkanPlayground main.cpp)

target_link_libraries(VulkanPlayground Vulkan glfw glm)