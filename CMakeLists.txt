# ./CMakeLists.txt
# Created by  2025-08-06
# License LGPL Open Source

cmake_minimum_required(VERSION 3.31)
set(CMAKE_C_STANDARD 23)
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

project(TinyCC)
message("Configuring ${CMAKE_PROJECT_NAME}...")
enable_testing()

set(ELF_FILES tccelf.c )
set(LIB_FILES libtcc.c )
set(CORE_FILES tcctools.c tccpp.c tccgen.c tccdbg.c tccasm.c tccrun.c
tcc.h config.h libtcc.h tcctok.h )
set(i386_FILES ${CORE_FILES} i386-gen.c i386-link.c i386-asm.c i386-asm.h i386-tok.h )
set(i386-win32_FILES ${i386_FILES} tccpe.c)
set(x86_64_FILES ${CORE_FILES} x86_64-gen.c x86_64-link.c i386-asm.c x86_64-asm.h )
set(x86_64-win32_FILES ${x86_64_FILES} tccpe.c )
set(x86_64-osx_FILES ${x86_64_FILES} tccmacho.c )
set(arm_FILES ${CORE_FILES} arm-gen.c arm-link.c arm-asm.c arm-tok.h )
set(arm-wince_FILES ${arm_FILES} tccpe.c)
#arm-eabihf_FILES = $(arm_FILES)
#arm-fpa_FILES     = $(arm_FILES)
#arm-fpa-ld_FILES  = $(arm_FILES)
#arm-vfp_FILES     = $(arm_FILES)
#arm-eabi_FILES    = $(arm_FILES)
#arm-eabihf_FILES  = $(arm_FILES)
set(arm64_FILES ${CORE_FILES} arm64-gen.c arm64-link.c arm64-asm.c )
set(arm64-osx_FILES ${arm64_FILES} tccmacho.c )
set(c67_FILES ${CORE_FILES} c67-gen.c c67-link.c tcccoff.c )
set(riscv64_FILES ${CORE_FILES} riscv64-gen.c riscv64-link.c riscv64-asm.c )
	
#define TCC_TARGET_X86_64 1
#define CONFIG_TRIPLET "x86_64-linux-gnu"

if(WIN32)
    message(STATUS "Building on Windows")
	set(SOURCES ${i386-win32_FILES} sources.cmake README.md)
	add_definitions(-DTCC_TARGET_X86_64=1 -DTCC_TARGET_PE -DPOINTER_SIZE=${CMAKE_SIZEOF_VOID_P}) #-DTARGET_DEFS_ONLY)
	add_definitions(-DCONFIG_TRIPLET="x86_64-windows")
elseif(APPLE)
    message(STATUS "Building on macOS")
elseif(UNIX)
    message(STATUS "Building on a Unix-like system (excluding macOS)")
#		set(SOURCES ${i386-win32_FILES} )
	add_definitions(-DTCC_TARGET_X86_64=1)
	add_definitions(-DCONFIG_TRIPLET="x86_64-linux-gnu")
else()
    message(STATUS "Building on an unknown OS")
endif()

if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
    message(STATUS "Specifically targeting Linux")
endif()

# arm) default triplet "arm-linux-androideabi"; cpuver=7 ;;
# arm64) default triplet "aarch64-linux-android" ;;
# x86_64) default triplet "x86_64-linux-android" ;;
#  i386) default triplet "i686-linux-android" ;;
#  default triplet "${cpu}-linux-gnu"

#define TCC_VERSION "0.9.28rc"
file(STRINGS VERSION TCC_VERSION)
add_definitions(-DTCC_VERSION="${TCC_VERSION}")

#ifndef CONFIG_TCCDIR
#define CONFIG_TCCDIR "/usr/local/lib/tcc"
#endif
#define CONFIG_TCC_PREDEFS 1

add_library(${PROJECT_NAME}_lib ${SOURCES})
link_libraries(${PROJECT_NAME}_lib)

if(NOT WIN32 AND NOT APPLE)
	link_libraries(rt pthread)
endif(NOT WIN32 AND NOT APPLE)

option(SUPPRESS "Suppress common VC++ legacy code warnings" false)
if(SUPPRESS)
	if(WIN32)
		add_definitions(-D_CRT_SECURE_NO_WARNINGS /wd4244 /wd4305 /wd4018 /wd26451 /wd6031 /wd4267)
	endif(WIN32)
endif(SUPPRESS)
#add_subdirectory(./examples)
#add_subdirectory(./include)
#add_subdirectory(./lib)
#add_subdirectory(./tests)
#add_subdirectory(./win32)

add_executable(c2str ./conftest.c)
add_executable(tcc ./tcc.c)