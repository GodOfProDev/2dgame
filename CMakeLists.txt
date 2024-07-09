cmake_minimum_required(VERSION 3.28)
project(2dgame C)

set(CMAKE_C_STANDARD 23)

# Add the path to SDL2 headers
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/vendor/SDL/include)

# Add the path to SDL2 libraries
link_directories(${CMAKE_CURRENT_SOURCE_DIR}/vendor/SDL/lib/x64)

# Add your source files
add_executable(2dgame src/main.c)

# Link SDL2 libraries
target_link_libraries(2dgame SDL2main SDL2)

# Copy SDL2.dll to the output directory (for Windows)
if(WIN32)
    add_custom_command(TARGET 2dgame POST_BUILD
            COMMAND ${CMAKE_COMMAND} -E copy_if_different
            "${CMAKE_CURRENT_SOURCE_DIR}/vendor/SDL/lib/x64/SDL2.dll"
            $<TARGET_FILE_DIR:2dgame>)
endif()