cmake_minimum_required(VERSION 2.8.5)
project(libsaturn)

# ensure that the cxx files get compiled with c++11 support enabled
set(CMAKE_CXX_FLAGS "--std=c++11 ${CMAKE_CXX_FLAGS}")

# ensure the linker can find libsaturn
include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/device)


# create a standalone library file for integration
set(SATURN_LIB_SRC ${CMAKE_CURRENT_SOURCE_DIR})
add_library (libsaturn
    ${SATURN_LIB_SRC}/libsaturn.cpp

    # device files
    ${SATURN_LIB_SRC}/device/clock.cpp
    ${SATURN_LIB_SRC}/device/keyboard.cpp
    ${SATURN_LIB_SRC}/device/lem1802.cpp
    ${SATURN_LIB_SRC}/device/m35fd.cpp
    ${SATURN_LIB_SRC}/device/disk.cpp
    ${SATURN_LIB_SRC}/device/fstream_disk.cpp
    ${SATURN_LIB_SRC}/device/mem_disk.cpp
    ${SATURN_LIB_SRC}/device/sped3.cpp

    # misc
    ${SATURN_LIB_SRC}/utilities.cpp
)
# ensure that the output file for libsaturn only contains one lib (ie, not liblibsaturn)
set_target_properties(libsaturn PROPERTIES PREFIX "")

