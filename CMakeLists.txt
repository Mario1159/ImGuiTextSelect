cmake_minimum_required(VERSION 3.16)
project(imguitextselect LANGUAGES CXX)

add_library(imguitextselect
    textselect.cpp
)

add_library(imguitextselect::imguitextselect ALIAS imguitextselect)

target_include_directories(imguitextselect
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
        $<INSTALL_INTERFACE:include>
)

# Link against existing Dear ImGui target
find_package(imgui CONFIG QUIET)

if(TARGET imgui::imgui)
    target_link_libraries(imguitextselect PUBLIC imgui::imgui)
elseif(TARGET imgui)
    target_link_libraries(imguitextselect PUBLIC imgui)
endif()

target_compile_features(imguitextselect PUBLIC cxx_std_11)
