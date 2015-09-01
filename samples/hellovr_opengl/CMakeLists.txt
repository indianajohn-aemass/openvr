cmake_minimum_required(VERSION 2.8)
PROJECT(hellovr-opengl)

FIND_PACKAGE(OpenGL REQUIRED)
INCLUDE_DIRECTORIES(OPENGL_INCLUDE_DIR)
INCLUDE_DIRECTORIES(GLUT_INCLUDE_DIR)
FIND_PACKAGE(GLUT REQUIRED)
if (NOT CONFIGURED_ONCE)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11"
            CACHE STRING "Flags used by the compiler during all build types." FORCE)
    SET(CONFIGURED_ONCE TRUE CACHE STRING "Configured at least once?")
endif()
if (APPLE)
    ADD_DEFINITIONS(-DMACOS)
ENDIF()

INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/../)
SET(OPENVR_API_LIB ${CMAKE_CURRENT_SOURCE_DIR}/../../lib/osx32/libopenvr_api.dylib)
INCLUDE_DIRECTORIES(SYSTEM ${CMAKE_CURRENT_SOURCE_DIR}/../../headers/)
SET(GLEW_LIB ${CMAKE_CURRENT_SOURCE_DIR}/../thirdparty/glew/glew-1.11.0/lib/Release/osx32/libGLEW.a)
INCLUDE_DIRECTORIES(SYSTEM ${CMAKE_CURRENT_SOURCE_DIR}/../thirdparty/glew/glew-1.11.0/include/)

INCLUDE(FindPkgConfig)
PKG_SEARCH_MODULE(SDL2 REQUIRED sdl2)
INCLUDE_DIRECTORIES(${SDL2_INCLUDE_DIRS})

ADD_EXECUTABLE(hellovr_opengl
    hellovr_opengl_main.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/../shared/Matrices.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/../shared/lodepng.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/../shared/pathtools.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/../shared/osxfilebridge.mm
)

SET(OSX_FRAMEWORKS "-framework CoreServices -framework AudioUnit -framework CoreAudio")

TARGET_LINK_LIBRARIES(hellovr_opengl ${OPENVR_API_LIB} ${GLEW_LIB} ${SDL2_LIBRARIES}
                                    ${GLUT_LIBRARIES} ${OPENGL_LIBRARIES}
                                    ${OSX_FRAMEWORKS})
