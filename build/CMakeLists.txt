# Set the hostname
set(CMAKE_SYSTEM_NAME Linux)
set(CMAKE_SYSTEM_PROCESSOR armv71)

# Define the toolchain path to make it easier for other configs
set(toolchainpath C:/build/18.0/arm/oecore-i686-cortexa9-vfpv3-toolchain-6.0/sysroots)

# Configure C/C++ compilers
set(CMAKE_C_COMPILER ${toolchainpath}/i686-nilrtsdk-mingw32/usr/bin/arm-nilrt-linux/arm-nilrt-linux-gcc.exe)
set(CMAKE_CXX_COMPILER ${toolchainpath}/i686-nilrtsdk-mingw32/usr/bin/arm-nilrt-linux/arm-nilrt-linux-g++.exe)

# Inlude sysroot and set compiler flags
set(CMAKE_SYSROOT ${toolchainpath}/cortexa9-vfpv3-nilrt-linux-gnueabi)
set(CMAKE_<LANG>_STANDARD_INCLUDE_DIRECTORIES ${toolchainpath}/cortexa9-vfpv3-nilrt-linuxgnueabi/usr/include/c++/6.3.0 ${toolchainpath}/cortexa9-vfpv3-nilrt-linuxgnueabi/usr/include/c++/6.3.0/arm-nilrt-linux-gnueabi)
set(CMAKE_<LANG>_FLAGS "-Wall -fmessage-length=0 -mfpu=vfpv3 -mfloat-abi=softfp")
set(CMAKE_<LANG>_FLAGS_DEBUG "-O0 -g3")
set(CMAKE_<LANG>_FLAGS_RELEASE "-O3")

# Don't unecessarily include extra files
set(CMAKE_FIND_ROOT_PATH_MODE_PROGRAM NEVER)
set(CMAKE_FIND_ROOT_PATH_MODE_LIBRARY ONLY)
set(CMAKE_FIND_ROOT_PATH_MODE_INCLUDE ONLY)
set(CMAKE_FIND_ROOT_PATH_MODE_PACKAGE ONLY)

# Update these to match your project
cmake_minimum_required(VERSION 3.14)
project(Template)

set(EXECUTABLE_OUTPUT_PATH bin)
set(CMAKE_BUILD_TYPE DEBUG)

add_executable(Template ../src/main.cpp)

include_directories(${toolchainpath}/cortexa9-vfpv3-nilrt-linux-gnueabi/usr/local/include)
include_directories(${toolchainpath}/cortexa9-vfpv3-nilrt-linux-gnueabi/usr/local/lib)

target_link_libraries(Template rioLib)