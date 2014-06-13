set(COMMON "${CMAKE_HOME_DIRECTORY}/src/common")

# Set sources
set(SRC invokelib.c invoker.c ${COMMON}/report.c search.c)

include(FindPkgConfig)
pkg_check_modules(SYSTEMD libsystemd-daemon)

# Set include dirs
include_directories(${CMAKE_CURRENT_SOURCE_DIR} ${SYSTEMD_INCLUDE_DIRS} ${COMMON})

# Set link libraries
link_libraries(${SYSTEMD_LDFLAGS})

# Set precompiler flags
add_definitions(-DPROG_NAME_INVOKER="invoker")

if (SYSTEMD_FOUND)
    add_definitions(-DHAVE_SYSTEMD)
endif (SYSTEMD_FOUND)

# Set target
add_executable(invoker ${SRC})

# Add install rule
install(PROGRAMS invoker DESTINATION /usr/bin/)


