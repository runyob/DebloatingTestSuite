# This is a master cmake script that will build all subprojects
# to produce a master list of binary test cases for ONR TPCP
# debloating research projects.
cmake_minimum_required (VERSION 3.16)
project (ONR_TPCP_TEST_SUITE)

# Recurse into subdirectories.
# Two rules:
# (1) if subproject uses cmake, simply recurse into it
# (2) if does not use cmake, use a custom command to
#     call the subproject's Make script, etc.

# add_custom_command(OUTPUT <output-file>
#                    COMMAND make run
#                    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/<subdir>
# )
# ---- or ----
# add_custom_target(<target_name> COMMAND make run
#                    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/<subdir>
# )
# ---- or ----
# add_subdirectory (sqlite)


file(MAKE_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/sqlite-build)
add_custom_command(OUTPUT sqlite3
                   COMMAND ${CMAKE_CURRENT_SOURCE_DIR}/sqlite/configure
                   COMMAND make
                   COMMAND make sqlite3.c
                   WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/sqlite-build
                   COMMENT "Building sqlite"
)

