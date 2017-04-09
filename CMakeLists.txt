cmake_minimum_required(VERSION 3.6)

project(nfd)

set(SOURCE_FILES
  	src/nfd_common.c
  	src/nfd_common.h)

if (WIN32)
  set(SOURCE_FILES ${SOURCE_FILES} src/nfd_win.cpp)
elseif (APPLE)
  set(SOURCE_FILES ${SOURCE_FILES} src/nfd_cocoa.m)
  set_source_files_properties(${SOURCE_FILES} PROPERTIES COMPILE_FLAGS "-x objective-c")
endif()

include_directories(src/include)

add_library(nfd ${SOURCE_FILES} )

install(TARGETS nfd DESTINATION lib)
install(FILES src/include/nfd.h DESTINATION include)
