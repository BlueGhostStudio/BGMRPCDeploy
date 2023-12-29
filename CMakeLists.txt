cmake_minimum_required(VERSION 3.18)

project(Deploy)

include(cmake/BGMRPC.cmake)

add_custom_target(
  Deploy ALL
  SOURCES BGMRPC.conf.in
          JsModules.conf.in
          bin/createAppJsObj
          bin/createAppObj
          bin/createAppPyObj
          bin/detachAppObj
          bin/restartApp
          bin/startApp
          bin/stopApp
          etc/IF_types.json)

configure_file(BGMRPC.conf.in ${CMAKE_CURRENT_BINARY_DIR}/etc/BGMRPC.conf @ONLY)
configure_file(JsModules.conf.in ${CMAKE_CURRENT_BINARY_DIR}/etc/JsModules.conf
               @ONLY)

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

install(
  DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/etc
  DESTINATION ${BGMRPC_REMOTE}/${CMAKE_INSTALL_DATADIR}
  COMPONENT BGMRPC_remote_deploy)
