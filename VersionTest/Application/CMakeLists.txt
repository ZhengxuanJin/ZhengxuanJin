cmake_minimum_required(VERSION 3.5.1)
project(VersionTest)

if(NOT TARGET Kanzi::kzappfw)
    find_package(Kanzi REQUIRED CONFIG CMAKE_FIND_ROOT_PATH_BOTH)
endif()

include(kanzi-common)

add_executable(VersionTest src/versiontest.cpp)

if(ANDROID)
    target_link_libraries(VersionTest -Wl,--whole-archive Kanzi::kzappfw -Wl,--no-whole-archive)
else()
    target_link_libraries(VersionTest Kanzi::kzappfw)
endif()

target_link_libraries(VersionTest Kanzi::kzui Kanzi::kzcoreui Kanzi::kzjs)

set_target_properties(VersionTest PROPERTIES VS_DEBUGGER_WORKING_DIRECTORY "${PROJECT_SOURCE_DIR}/bin")
