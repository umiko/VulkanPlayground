#a simple cmake file finding the required libraries for the Vulkan  tutorial
cmake_minimum_required(VERSION 3.13)
project(VulkanPlayground)

set(CMAKE_CXX_STANDARD 17)

find_package(Vulkan REQUIRED)
if(${Vulkan_FOUND})
    message('Found Vulkan, will try finding the remaining stuff')
    if (UNIX)
        find_package(glm REQUIRED)
        find_package(glfw3 REQUIRED)
    endif ()

    if(WIN32)
        add_subdirectory($ENV{glm_DIR} cmake-build-debug/glm)
        include_directories(${Vulkan_INCLUDE_DIRS})
        add_subdirectory($ENV{glfw_DIR} cmake-build-debug/glfw)
    endif()
else()
    message('Vulkan not found')
endif()

add_executable(VulkanPlayground main.cpp)

target_link_libraries(VulkanPlayground ${Vulkan_LIBRARIES} glfw glm)