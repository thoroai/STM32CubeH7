 # add qspi CMSIS includes here
if(P32_BOOTCODE)

    add_library(
        CMSIS_bootcode
        INTERFACE
    )
    target_include_directories(
        CMSIS_bootcode
        INTERFACE
        ${CMAKE_CURRENT_SOURCE_DIR}/Include
        ${CMAKE_CURRENT_SOURCE_DIR}/Device/ST/STM32H7xx/Include
    )
endif()

if(QSPI_EXTLOADER)
    # add Include dirs to target includes
    include_directories(
    
    ${CMAKE_CURRENT_SOURCE_DIR}Include
    )
endif()