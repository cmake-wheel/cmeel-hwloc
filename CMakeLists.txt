cmake_minimum_required(VERSION 3.30)

set(NAME hwloc)
set(VERSION 2.11.2)
set(EXT tar.gz)
set(SHA256 866ac8ef07b350a6a2ba0c6826c37d78e8994dcbcd443bdd2b436350de19d540)

project(cmeel-${NAME} VERSION ${VERSION})

include(ExternalProject)
ExternalProject_Add(
  ${NAME}
  URL "https://download.open-mpi.org/release/${NAME}/v2.11/${NAME}-${VERSION}.${EXT}"
  URL_HASH "SHA256=${SHA256}"
  BUILD_IN_SOURCE ON
  DOWNLOAD_EXTRACT_TIMESTAMP OFF
  CONFIGURE_COMMAND "./configure" "--prefix=${CMAKE_INSTALL_PREFIX}"
  BUILD_COMMAND "make"
  INSTALL_COMMAND "make" "install"
  COMMAND "${CMAKE_COMMAND}" "-E" "rm"
          "${CMAKE_INSTALL_PREFIX}/lib/lib${NAME}.la")

# dummy file for install target
install(FILES "README.md" DESTINATION "share/cmeel-${NAME}/")
