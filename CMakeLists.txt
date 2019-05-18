#a simple cmake file finding the required libraries for the Vulkan  tutorial
cmake_minimum_required(VERSION 3.13)
project(VulkanPlayground)

set(CMAKE_CXX_STANDARD 17)

find_package(Vulkan REQUIRED)
if(${Vulkan_FOUND})
    message("Found Vulkan")
    if (UNIX)
        find_package(glm REQUIRED)

        if (!${GLM_FOUND})
            message("Please install 'libglm-dev'")
        else()
            message("Found glm")
        endif ()

        find_package(glfw3 REQUIRED)

        if (!${GLFW_FOUND})
            message("Please install 'libglfw3' and 'libglfw3-dev'")
        else()
            message("Found glfw3")
        endif ()

    endif ()

    if(WIN32)
        #requires glm_DIR to point to the glm root directory
        add_subdirectory($ENV{glm_DIR} cmake-build-debug/glm)
        #when building glfw, include directories ahve to be included before glfw
        include_directories(${Vulkan_INCLUDE_DIRS})
        #requires glfw_DIR to point to the glfw3 root directory
        add_subdirectory($ENV{glfw_DIR} cmake-build-debug/glfw)
    endif()

else()
    message("Vulkan not found, please make sure you installed the dependencies")
endif()

add_executable(VulkanPlayground main.cpp)

target_link_libraries(VulkanPlayground ${Vulkan_LIBRARIES} glfw glm)