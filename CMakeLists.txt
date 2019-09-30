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

#    if(WIN32)
#        add_library(glm INTERFACE)
#        target_include_directories(glm INTERFACE $ENV{glm_DIR})
#        add_library(glfw STATIC IMPORTED "C:/Program Files (x86)/glfw-3.3/lib/libglfw3.a")
#        include_directories("C:/Program Files (x86)/glfw-3.3/include")
#        include_directories(${Vulkan_INCLUDE_DIRS})
#    endif()

    if(WIN32)
        add_library(glm INTERFACE)
        target_include_directories(glm INTERFACE $ENV{glm_DIR})
        add_library(glfw STATIC IMPORTED "C:/Program Files (x86)/glfw-3.3/lib/libglfw3.a")
        include_directories("C:/Program Files (x86)/glfw-3.3/include")
        include_directories(${Vulkan_INCLUDE_DIRS})
    endif()

else()
    message("Vulkan not found, please make sure you installed the dependencies")
endif()

add_executable(VulkanPlayground main.cpp)

target_link_libraries(VulkanPlayground ${Vulkan_LIBRARIES} "C:/Program Files (x86)/glfw-3.3/lib/libglfw3.a" glm)