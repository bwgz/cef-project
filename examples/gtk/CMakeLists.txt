# Copyright (c) 2017 The Chromium Embedded Framework Authors. All rights
# reserved. Use of this source code is governed by a BSD-style license that
# can be found in the LICENSE file.


# Use the package PkgConfig to detect GTK+ headers/library files
find_package(PkgConfig REQUIRED)
pkg_check_modules(GTKMM REQUIRED gtkmm-3.0)

#
# Source files.
#

# Main executable sources.
set(EXAMPLE_SRCS
  window.cc
  window.h
  main.cc
  )
APPEND_PLATFORM_SOURCES(EXAMPLE_SRCS)
  
# Main executable resources.
set(EXAMPLE_RESOURCES_SRCS
  )
APPEND_PLATFORM_SOURCES(EXAMPLE_RESOURCES_SRCS)


#
# Shared configuration.
#

# Target executable names.
set(EXAMPLE_TARGET "gtk_cef")


#
# Linux configuration.
#

if(OS_LINUX)
  # Executable target.
  add_executable(${EXAMPLE_TARGET} ${EXAMPLE_SRCS})
  SET_EXAMPLE_EXECUTABLE_TARGET_PROPERTIES(${EXAMPLE_TARGET})
  add_dependencies(${EXAMPLE_TARGET} shared)
  target_include_directories(${EXAMPLE_TARGET} PRIVATE ${GTKMM_INCLUDE_DIRS})
  target_compile_options(${EXAMPLE_TARGET} PRIVATE ${GTKMM_CFLAGS_OTHER} -frtti -fexceptions)
  target_link_libraries(${EXAMPLE_TARGET} PUBLIC shared)
  target_link_libraries(${EXAMPLE_TARGET} PRIVATE ${GTKMM_LIBRARIES})
  target_link_directories(${EXAMPLE_TARGET} PRIVATE ${GTKMM_LIBRARY_DIRS})
endif()


