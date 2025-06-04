cmake_minimum_required(VERSION 3.16)
project(DoodleJump)

find_package(SFML REQUIRED COMPONENTS network audio graphics window system)

file(COPY "${CMAKE_CURRENT_SOURCE_DIR}/images" DESTINATION "${CMAKE_CURRENT_BINARY_DIR}/")

add_executable(doodle_jump main.cpp)

target_link_libraries(doodle_jump PRIVATE sfml-system sfml-window sfml-graphics sfml-network sfml-audio)

include(InstallRequiredSystemLibraries)

set(CPACK_PACKAGE_NAME "DoodleJump")
set(CPACK_PACKAGE_VENDOR "YourCompany")
set(CPACK_PACKAGE_VERSION "1.0.0")
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "Doodle Jump Game")
set(CPACK_PACKAGE_INSTALL_DIRECTORY "DoodleJump")

install(TARGETS doodle_jump
    RUNTIME DESTINATION "."
    BUNDLE DESTINATION "."
)

install(DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/images/"
    DESTINATION "images"
)

install(CODE "
    file(GLOB SFML_DLLS \"${SFML_DIR}/bin/*.dll\")
    file(COPY \${SFML_DLLS} DESTINATION \"\${CMAKE_INSTALL_PREFIX}\")
")

include(CPack)


