add_library(
    freeRTOS_includes
    INTERFACE
)

target_include_directories(
    freeRTOS_includes
    INTERFACE
    ${CMAKE_CURRENT_SOURCE_DIR}
)