cmake_minimum_required (VERSION 2.8)

project (GLSLCOOKBOOK)

set( CMAKE_MODULE_PATH ${GLSLCOOKBOOK_SOURCE_DIR}/cmake/modules )

IF(NOT CMAKE_BUILD_TYPE)
  SET(CMAKE_BUILD_TYPE RelWithDebInfo CACHE STRING
      "Choose the type of build, options are: None Debug Release RelWithDebInfo MinSizeRel."
      FORCE)
ENDIF(NOT CMAKE_BUILD_TYPE)

find_package( GLM REQUIRED )
find_package( GLFW3 REQUIRED )

set( GLSLCOOKBOOK_LIBS ingredients )
set( GLSLCOOKBOOK_INCLUDE ${GLSLCOOKBOOK_SOURCE_DIR}/ingredients )

list( APPEND GLSLCOOKBOOK_INCLUDE ${GLM_INCLUDE_DIRS} )
list( APPEND GLSLCOOKBOOK_INCLUDE ${GLFW3_INCLUDE_DIR} )
list( APPEND GLSLCOOKBOOK_LIBS ${GLFW3_LIBRARY} )

if( APPLE )
  add_definitions(-Wall)

  find_library( APPLE_OPENGL OpenGL )
  find_library( APPLE_COCOA Cocoa )
  find_library( APPLE_IO IOKit )
  find_library( APPLE_CORE_FOUNDATION_FRAMEWORK CoreFoundation)
  find_library( APPLE_CORE_VIDEO_FRAMEWORK CoreVideo)

  list( APPEND GLSLCOOKBOOK_LIBS  ${APPLE_COCOA} ${APPLE_IO} ${APPLE_CORE_FOUNDATION_FRAMEWORK} ${APPLE_CORE_VIDEO_FRAMEWORK})
elseif( UNIX )
  add_definitions(-Wall)

  find_package( X11 REQUIRED )
  find_package( OpenGL REQUIRED )
  find_package( Threads REQUIRED )

  list( APPEND GLSLCOOKBOOK_LIBS ${X11_X11_LIB} ${X11_Xrandr_LIB} ${X11_Xinerama_LIB} ${X11_Xi_LIB} ${X11_Xxf86vm_LIB} ${X11_Xcursor_LIB} ${OPENGL_gl_LIBRARY} ${CMAKE_DL_LIBS} ${CMAKE_THREAD_LIBS_INIT})
elseif( WIN32 )
  find_package( OpenGL REQUIRED )
  list( APPEND GLSLCOOKBOOK_LIBS ${OPENGL_gl_LIBRARY} )
endif()

include_directories( ${GLSLCOOKBOOK_INCLUDE} )

add_subdirectory( ingredients )
add_subdirectory( chapter01 )
add_subdirectory( chapter02 )
add_subdirectory( chapter03 )
add_subdirectory( chapter04 )
add_subdirectory( chapter05 )
add_subdirectory( chapter06 )
add_subdirectory( chapter07 )
add_subdirectory( chapter08 )
add_subdirectory( chapter09 )
add_subdirectory( chapter10 )

file(COPY ${CMAKE_CURRENT_SOURCE_DIR}/media DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
