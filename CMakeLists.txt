cmake_minimum_required(VERSION 3.18)

project(Deploy)

include(cmake/BGMRPC.cmake)

add_custom_target(
  Deploy ALL
  COMMAND ${CMAKE_COMMAND} -E copy_directory ${CMAKE_CURRENT_LIST_DIR}/etc
          ${CMAKE_CURRENT_BINARY_DIR}/etc
  COMMAND ${CMAKE_COMMAND} -E copy_directory ${CMAKE_CURRENT_LIST_DIR}/bin
          ${CMAKE_CURRENT_BINARY_DIR}/bin)

#target_sources(
#  Deploy
#  PRIVATE bin/createAppJsObj
#          bin/createAppObj
#          bin/createAppPyObj
#          bin/detachAppObj
#          bin/restartApp
#          bin/startApp
#          bin/stopApp
#          etc/BGMRPC.conf
#          etc/JsModules.conf)

install(
  DIRECTORY bin
  DESTINATION ${BGMRPC_REMOTE}
  COMPONENT BGMRPC_remote_deploy
  PATTERN
    "bin/*"
    PERMISSIONS
      OWNER_EXECUTE
      OWNER_WRITE
      OWNER_READ
      GROUP_EXECUTE
      GROUP_READ
      WORLD_EXECUTE
      WORLD_READ)

install(
  DIRECTORY etc
  DESTINATION ${BGMRPC_REMOTE}/${CMAKE_INSTALL_DATADIR}
  COMPONENT BGMRPC_remote_deploy)
