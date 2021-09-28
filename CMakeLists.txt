cmake_minimum_required(VERSION 3.5)

project(ggk LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(PkgConfig REQUIRED)
find_package(Threads REQUIRED)

pkg_search_module(GLib REQUIRED glib-2.0)
pkg_search_module(GIO REQUIRED gio-unix-2.0)

include_directories(${GLib_INCLUDE_DIRS}
                    ${GIO_INCLUDE_DIRS})

link_directories(${GLib_LIBRARY_DIRS}
                ${GIO_LIBRARY_DIRS})

set (ggk_LIB_SRCS
  ${PROJECT_SOURCE_DIR}/src/DBusInterface.cpp
  ${PROJECT_SOURCE_DIR}/src/DBusMethod.cpp
  ${PROJECT_SOURCE_DIR}/src/DBusObject.cpp
  ${PROJECT_SOURCE_DIR}/src/GattCharacteristic.cpp
  ${PROJECT_SOURCE_DIR}/src/GattDescriptor.cpp
  ${PROJECT_SOURCE_DIR}/src/GattInterface.cpp
  ${PROJECT_SOURCE_DIR}/src/GattProperty.cpp
  ${PROJECT_SOURCE_DIR}/src/GattService.cpp
  ${PROJECT_SOURCE_DIR}/src/Gobbledegook.cpp
  ${PROJECT_SOURCE_DIR}/src/HciAdapter.cpp
  ${PROJECT_SOURCE_DIR}/src/HciSocket.cpp
  ${PROJECT_SOURCE_DIR}/src/Init.cpp
  ${PROJECT_SOURCE_DIR}/src/Logger.cpp
  ${PROJECT_SOURCE_DIR}/src/Mgmt.cpp
  ${PROJECT_SOURCE_DIR}/src/Server.cpp
  ${PROJECT_SOURCE_DIR}/src/ServerUtils.cpp
  ${PROJECT_SOURCE_DIR}/src/Utils.cpp
)

add_library(ggk ${ggk_LIB_SRCS})

target_link_libraries(ggk
                      ${GLib_LIBRARIES}
                      ${GIO_LIBRARIES}
                      pthread
                     )
