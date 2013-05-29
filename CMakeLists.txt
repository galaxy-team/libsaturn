cmake_minimum_required(VERSION 2.8.5)
project(libsaturn)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)

# ensure that the cxx files get compiled with c++11 support enabled
set(CMAKE_CXX_FLAGS "--std=c++11 ${CMAKE_CXX_FLAGS}")

# ensure the linker can find libsaturn
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

# create a standalone library file for integration
set(SATURN_LIB_SRC ${CMAKE_CURRENT_SOURCE_DIR})
add_library (libsaturn
    ${SATURN_LIB_SRC}/src/dcpu.cpp

    # device files
    ${SATURN_LIB_SRC}/src/device/clock.cpp
    ${SATURN_LIB_SRC}/src/device/keyboard.cpp
    ${SATURN_LIB_SRC}/src/device/lem1802.cpp
    ${SATURN_LIB_SRC}/src/device/m35fd.cpp
    ${SATURN_LIB_SRC}/src/device/disk.cpp
    ${SATURN_LIB_SRC}/src/device/fstream_disk.cpp
    ${SATURN_LIB_SRC}/src/device/mem_disk.cpp
    ${SATURN_LIB_SRC}/src/device/sped3.cpp

    # misc
    ${SATURN_LIB_SRC}/src/utilities.cpp
)
# ensure that the output file for libsaturn only contains one lib (ie, not liblibsaturn)
set_target_properties(libsaturn PROPERTIES PREFIX "")

## if testing has been enabled, build the tests and run them! :D
add_executable(tests
    ${CMAKE_CURRENT_SOURCE_DIR}/tests/tests.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/tests/test_device.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/tests/units/test_disk.cpp
)
target_link_libraries(tests libsaturn)

