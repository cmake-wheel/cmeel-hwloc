cmake_minimum_required(VERSION 3.20)

set(NAME hwloc)
set(VERSION 2.9.2)

project(cmeel-${NAME} VERSION ${VERSION})

include(ExternalProject)
ExternalProject_Add(
  ${NAME}
  URL "https://download.open-mpi.org/release/${NAME}/v2.9/${NAME}-${VERSION}.tar.bz2"
  BUILD_IN_SOURCE ON
  DOWNLOAD_EXTRACT_TIMESTAMP OFF
  CONFIGURE_COMMAND "./configure" "--prefix=${CMAKE_INSTALL_PREFIX}"
  BUILD_COMMAND "make"
  INSTALL_COMMAND "make" "install"
  COMMAND "${CMAKE_COMMAND}" "-E" "rm" "${CMAKE_INSTALL_PREFIX}/lib/lib${NAME}.la")

# dummy file for install target
install(FILES README.md DESTINATION share/cmeel-${NAME}/)
