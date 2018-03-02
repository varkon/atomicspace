cmake_minimum_required(VERSION 3.5)

file(GLOB_RECURSE HEADERS "*.h")
file(GLOB SOURCES "*.cpp")


set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)

find_package(Qt5Core REQUIRED)
find_package(Qt5Gui REQUIRED)
find_package(Qt5Widgets REQUIRED)

set(CARLO_DIR /usr/local/ha-sdk)
list(APPEND SOURCES ../../../common/Qt/ManeuverHelper.cpp)

set(TARGET_NAME QtGuidanceSample)
link_directories (${CARLO_DIR}/lib)

add_executable(${TARGET_NAME} ${SOURCES})

find_library(COMMON_LIB_LOCATION libcommon.a)

target_link_libraries(${TARGET_NAME}
    carlo-navcore
    carlo-utilities
    Qt5::Core
    Qt5::Gui
    Qt5::Widgets
    ${CARLO_DIR}/lib/libcommon.a
)

target_include_directories(${TARGET_NAME} PRIVATE
    .
#    ${CARLO_DIR}/samples/common/Qt
    ${CARLO_DIR}/include
    ${CMAKE_BINARY_DIR}
    ../../../common/Qt
)
