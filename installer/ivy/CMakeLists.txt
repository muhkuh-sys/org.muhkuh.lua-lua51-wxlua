cmake_minimum_required(VERSION 3.0)

PROJECT("wxlua")

INCLUDE(ExternalProject)

# Get the VCS version.
INCLUDE(../../cmake/version.cmake)

# Get the version of the package.
GET_FILENAME_COMPONENT(CMAKE_PREFIX_PATH "../../build_windows32/lua/install" ABSOLUTE)
SET(org.muhkuh.lua-lua51-wxlua_VERSION "2.8.12")


SET(PACKAGE_CMAKE_ARGS "")
LIST(APPEND PACKAGE_CMAKE_ARGS "-DVERSION_FULL=${org.muhkuh.lua-lua51-wxlua_VERSION}")
LIST(APPEND PACKAGE_CMAKE_ARGS "-DPROJECT_VERSION_VCS=${PROJECT_VERSION_VCS}")
LIST(APPEND PACKAGE_CMAKE_ARGS "-DARTIFACT_LISTS_OUTPUT=${CMAKE_CURRENT_BINARY_DIR}/artifacts")

ExternalProject_Add(TARGET_wxlua
                    SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/wxlua
                    CMAKE_ARGS ${PACKAGE_CMAKE_ARGS}
                    INSTALL_COMMAND make package
)

# Create a copy of the artifacts without a version number in the filename.
# This allows easy deploy to GitHub.
INSTALL(FILES ${CMAKE_CURRENT_BINARY_DIR}/TARGET_wxlua-prefix/src/TARGET_wxlua-build/lua51-wxlua-${org.muhkuh.lua-lua51-wxlua_VERSION}.zip
        DESTINATION ${CMAKE_CURRENT_BINARY_DIR}
        RENAME lua51-wxlua.zip)
INSTALL(FILES ${CMAKE_CURRENT_BINARY_DIR}/TARGET_wxlua-prefix/src/TARGET_wxlua-build/ivy-${org.muhkuh.lua-lua51-wxlua_VERSION}.xml
        DESTINATION ${CMAKE_CURRENT_BINARY_DIR}
        RENAME ivy.xml)

#----------------------------------------------------------------------------

