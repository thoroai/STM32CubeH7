 # add qspi CMSIS includes here

if(QSPI_EXTLOADER)
    # add Include dirs to target includes
    include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/Device/ST/STM32H7xx/Include
    ${CMAKE_CURRENT_SOURCE_DIR}Include
    )
endif()