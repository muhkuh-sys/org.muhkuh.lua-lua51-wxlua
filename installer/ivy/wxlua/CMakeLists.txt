cmake_minimum_required(VERSION 2.8)

SET(CPACK_INCLUDE_TOPLEVEL_DIRECTORY FALSE)
SET(CPACK_PACKAGE_FILE_NAME lua51-wxlua-${VERSION_FULL})

SET(CPACK_GENERATOR "ZIP")
INCLUDE(CPack)

# Build the ivy file.
CONFIGURE_FILE(ivy.xml ivy-${VERSION_FULL}.xml)

#-----------------------------------------------------------------------------
#
# Install the 32bit files.
#
INSTALL(FILES /usr/local/mingw-w64-i686/bin/libwx.dll
        RENAME wx.dll
        DESTINATION windows_x86
)


#-----------------------------------------------------------------------------
#
# Install the 64bit files.
#
INSTALL(FILES /usr/local/mingw-w64-x86_64/bin/libwx.dll
        RENAME wx.dll
        DESTINATION windows_amd64
)


#-----------------------------------------------------------------------------

INSTALL(FILES install.xml
        DESTINATION .)


#-----------------------------------------------------------------------------
#
# Filter the pom.xml file.
#
SET(POM_ARTIFACT_ID  "lua51-wxlua")
SET(POM_GROUP_ID     "lua.muhkuh.org")
SET(POM_VERSION      "${VERSION_FULL}")
SET(POM_PACKAGING    "zip")
CONFIGURE_FILE(${CMAKE_CURRENT_SOURCE_DIR}/../pom.xml pom.xml)


#-----------------------------------------------------------------------------
#
# Filter the artifacts.xml file.
#
SET(ARTIFACT_DIRECTORY    "${CMAKE_CURRENT_BINARY_DIR}")
SET(ARTIFACT_ARTIFACT_ID  "lua51-wxlua")
SET(ARTIFACT_GROUP_ID     "lua.muhkuh.org")
SET(ARTIFACT_VERSION      "${VERSION_FULL}")
CONFIGURE_FILE(${CMAKE_CURRENT_SOURCE_DIR}/../artifacts.xml ${ARTIFACT_LISTS_OUTPUT}/artifacts_wxlua.xml)

