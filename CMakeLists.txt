cmake_minimum_required(VERSION 3.12)
project(qc_devcfg_parser VERSION 0.1 LANGUAGES C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Wextra -Werror")
set(CMAKE_CXX_FLAGS "${CMAKE_C_FLAGS} -Wall -Wextra -Werror")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-nonnull-compare")
set(DEFAULT_ENABLE_LTO     ON)
set(DEFAULT_ENABLE_QT      ON)
set(DEFAULT_ENABLE_STATIC  ON)
if(CMAKE_BUILD_TYPE STREQUAL "Release")
	add_definitions(-Os)
	set(DEFAULT_ENABLE_LTO ON)
endif()
find_package(QT NAMES Qt6 Qt5)
if(QT_FOUND)
	set(DEFAULT_ENABLE_QT ON)
endif()
option(ENABLE_QT     "Build QT Gui"              ${DEFAULT_ENABLE_QT})
option(ENABLE_STATIC "Enable static link"        ${DEFAULT_ENABLE_STATIC})
option(ENABLE_LTO    "Enable link time optimize" ${DEFAULT_ENABLE_LTO})
set(INCBIN_FILE "${CMAKE_CURRENT_SOURCE_DIR}/src/incbin.s.in")
include_directories(include)
add_subdirectory(po)
add_subdirectory(src)
