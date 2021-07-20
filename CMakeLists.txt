cmake_minimum_required(VERSION 3.8)

project(vulkan_game VERSION 0.1.0)
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Download automatically, you can also just copy the conan.cmake file
if(NOT EXISTS "${CMAKE_BINARY_DIR}/conan.cmake")
message(STATUS "Downloading conan.cmake from https://github.com/conan-io/cmake-conan")
    file(DOWNLOAD "https://raw.githubusercontent.com/conan-io/cmake-conan/v0.9/conan.cmake"
                "${CMAKE_BINARY_DIR}/conan.cmake")
endif()

include(${CMAKE_BINARY_DIR}/conan.cmake)
conan_cmake_run(
			CONANFILE conanfile.txt
			BASIC_SETUP CMAKE_TARGETS 
			# BUILD_TYPE "Debug"
			)
			
conan_set_find_library_paths()

set(CMAKE_BINARY_DIR ${CMAKE_BINARY_DIR}/bin)
message(${CMAKE_BINARY_DIR})

include(CTest)
enable_testing()

add_executable(vulkan_game 
    Source.cpp
    AppValidationLayersAndExtensions.cpp
    Device.cpp
    VulkanContext.cpp
    VulkanInstance.cpp
)

target_link_libraries(${PROJECT_NAME} 
    vulkan
    CONAN_PKG::glfw
    )

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
