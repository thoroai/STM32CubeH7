add_library(
    RTOS2_includes
    INTERFACE
)

message("RTOS2_includes_lib building")
target_include_directories(
    RTOS2_includes
    INTERFACE
    ${CMAKE_CURRENT_SOURCE_DIR}/Include
)