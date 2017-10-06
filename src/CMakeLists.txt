cmake_minimum_required(VERSION 3.1.0 FATAL_ERROR)
project(core C)

if(LIBUX_ENABLE_SHARED_BUILD)
  add_definitions(-DUX_BUILD_SHARED -DUX_BUILD_LIBRARY)
  set(LIBUX_BUILD_TYPE SHARED)
else()
  add_definitions(-DUX_BUILD_LIBRARY)
  set(LIBUX_BUILD_TYPE STATIC)
endif()

if(NOT WIN32)
  add_definitions(-DDLOPEN_POSIX)
endif()

set(UX_CORE_HEADER

)

set(UX_CORE_SRC
        cp.c
        cp_context.c
        cp_hash.c
        cp_list.c
        cp_logging.c
        cp_descriptor.c
        cp_info.c
        cp_loader.c
        cp_control.c
        cp_scan.c
        cp_symbol.c
        cp_serial.c
        cp_util.c
)

if(WIN32)
  list(APPEND UX_CORE_SRC thread_windows.c)
else(WIN32)
  list(APPEND UX_CORE_SRC thread_posix.c)
endif()

add_library(cpcore ${LIBUX_BUILD_TYPE}  ${UX_CORE_HEADER} ${UX_CORE_SRC})
target_link_libraries(cpcore ${UX_EXTERNAL_LIBRARIES})
