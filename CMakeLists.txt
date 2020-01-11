cmake_minimum_required(VERSION 3.2)

# NOTICE: This file is a wrapper around the original 'CMakeLists.txt' which was
# renamed to 'CMakeLists.txt.orig'

include(CMakeLists.txt.orig)

install(
  EXPORT mbedtls-targets
  DESTINATION lib/cmake/mbedtls
  NAMESPACE mbedtls::)
export(PACKAGE mbedtls)

set(pkg_cfg ${PROJECT_BINARY_DIR}/pkgcfg.cmake.in)
file(WRITE ${pkg_cfg} 
    "# mbedtls-config.cmake
# get deps
find_package(ZLIB)
get_filename_component(MBEDTLS_CMAKE_DIR \${CMAKE_CURRENT_LIST_FILE} PATH)
include(\${MBEDTLS_CMAKE_DIR}/mbedtls-targets.cmake)
")

install(
  FILES ${pkg_cfg}
  DESTINATION lib/cmake/mbedtls
  RENAME mbedtls-config.cmake
  COMPONENT dev)
