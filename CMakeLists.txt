cmake_minimum_required(VERSION 3.10)

project(HUACA
  VERSION 0.1.0
)

include(GNUInstallDirs)

find_package(gf REQUIRED COMPONENTS graphics)

set(HUACA_DATA_DIR "${CMAKE_INSTALL_PREFIX}/share/games/huaca")
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/code/config.h.in ${CMAKE_CURRENT_BINARY_DIR}/config.h @ONLY)

add_executable(huaca
  code/huaca.cc
  code/local/Display.cc
  code/local/Hero.cc
  code/local/Level.cc
  code/local/Singletons.cc
  code/local/Timer.cc
)

target_include_directories(huaca
  PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/code
    ${CMAKE_CURRENT_BINARY_DIR}
)

target_link_libraries(huaca
  PRIVATE
    gf::graphics
)

install(
  TARGETS huaca
  RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
)

install(
  DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/data/huaca"
  DESTINATION "${CMAKE_INSTALL_DATAROOTDIR}/games"
)
