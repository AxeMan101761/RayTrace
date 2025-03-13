cmake_minimum_required ( VERSION 3.1.0...3.27.0 )

project ( RTWeekend LANGUAGES CXX )

# Set to C++11
set ( CMAKE_CXX_STANDARD          11 )
set ( CMAKE_CXX_STANDARD_REQUIRED ON )
set ( CMAKE_CXX_EXTENSIONS        OFF )

# Source
# Reference the correct path to main.cpp based on its location in the runfiles folder
set ( SOURCES
  runfiles/main.cpp
)

# Compiler flags (optional, can be customized based on your setup)
message (STATUS "Compiler ID: " ${CMAKE_CXX_COMPILER_ID})
message (STATUS "Release flags: " ${CMAKE_CXX_FLAGS_RELEASE})
message (STATUS "Debug flags: " ${CMAKE_CXX_FLAGS_DEBUG})

if (CMAKE_CXX_COMPILER_ID STREQUAL "MSVC")
    add_compile_options("/W4") # Enable level-4 warnings
elseif (CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
    add_compile_options(-Wnon-virtual-dtor)
    add_compile_options(-Wreorder)
    add_compile_options(-Wmaybe-uninitialized)
    add_compile_options(-Wunused-variable)
elseif (CMAKE_CXX_COMPILER_ID MATCHES "Clang")
    add_compile_options(-Wnon-virtual-dtor)
    add_compile_options(-Wreorder)
    add_compile_options(-Wsometimes-uninitialized)
    add_compile_options(-Wunused-variable)
endif()

# Executable
add_executable(RayTracing ${SOURCES})
