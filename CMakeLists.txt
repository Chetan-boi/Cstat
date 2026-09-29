cmake_minimum_required(VERSION 3.20)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

project(Cstat LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Dependencies: GLFW via Homebrew
find_package(glfw3 3.3 REQUIRED)
find_package(OpenGL REQUIRED)

# ImGui source location (assumes imgui is vendored in external/imgui or similar)
set(IMGUI_DIR "${CMAKE_CURRENT_SOURCE_DIR}/external/imgui")

set(IMGUI_SOURCES
    ${IMGUI_DIR}/imgui.cpp
    ${IMGUI_DIR}/imgui_demo.cpp
    ${IMGUI_DIR}/imgui_draw.cpp
    ${IMGUI_DIR}/imgui_tables.cpp
    ${IMGUI_DIR}/imgui_widgets.cpp
    ${IMGUI_DIR}/backends/imgui_impl_glfw.cpp
    ${IMGUI_DIR}/backends/imgui_impl_opengl3.cpp
)

add_executable(Cstat
    src/main.cpp
    ${IMGUI_SOURCES}
)

target_include_directories(Cstat PRIVATE
    include
    ${IMGUI_DIR}
    ${IMGUI_DIR}/backends
)

target_link_libraries(Cstat PRIVATE
    glfw
    OpenGL::GL
    "-framework Cocoa"
    "-framework IOKit"
    "-framework CoreVideo"
)
