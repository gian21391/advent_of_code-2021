cmake_minimum_required(VERSION 3.18)
set(CMAKE_TOOLCHAIN_FILE "$ENV{HOME}/.local/share/vcpkg/scripts/buildsystems/vcpkg.cmake" CACHE STRING "")
project(advent_of_code_21)

set(CMAKE_CXX_STANDARD 20)

find_package(fmt CONFIG REQUIRED)
find_package(Catch2 CONFIG REQUIRED)
find_package(Boost REQUIRED graph)


file(GLOB_RECURSE files RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} day*/*.cpp)
foreach(file ${files})
    string(REGEX REPLACE "\\/.*.[^.]*$" "" folder_name ${file})
    string(REPLACE / _ executable_name ${file})
    string(REGEX REPLACE "\\.[^.]*$" "" executable_name ${executable_name})
    add_executable(${executable_name} ${CMAKE_CURRENT_SOURCE_DIR}/${file})
    target_include_directories(${executable_name} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
    target_link_libraries(${executable_name} Catch2::Catch2 fmt::fmt Boost::graph)
endforeach()