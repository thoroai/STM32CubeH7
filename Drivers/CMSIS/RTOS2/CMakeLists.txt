add_library(
    RTOS2_includes
    INTERFACE
)

target_include_directories(
    RTOS2_includes
    INTERFACE
    ${CMAKE_CURRENT_SOURCE_DIR}/Include
    ${CMAKE_CURRENT_SOURCE_DIR}/Template
)