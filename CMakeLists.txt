cmake_minimum_required(VERSION 3.27)
project(polylabel VERSION 1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(polylabel INTERFACE)

target_include_directories(polylabel
  INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include/mapbox>
)

include(CMakePackageConfigHelpers)
configure_package_config_file(
  "${CMAKE_CURRENT_SOURCE_DIR}/polylabelConfig.cmake.in"
  "${CMAKE_CURRENT_BINARY_DIR}/polylabelConfig.cmake"
  INSTALL_DESTINATION share/polylabel
)

install(TARGETS polylabel
  EXPORT polylabelTargets
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)

install(DIRECTORY
  "${CMAKE_CURRENT_SOURCE_DIR}/include/mapbox"
  DESTINATION include/mapbox
)

install(
  EXPORT polylabelTargets
  DESTINATION share/polylabel
  NAMESPACE polylabel::
)

install(
  FILES
  "${CMAKE_CURRENT_BINARY_DIR}/polylabelConfig.cmake"
  DESTINATION share/polylabel
)