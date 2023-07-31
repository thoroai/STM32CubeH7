

if(P32_BOOTCODE)
endif()

if(QSPI_EXTLOADER)

#add the following dirs to includes
    ${CMAKE_CURRENT_SOURCE_DIR}/include
    ${CMAKE_CURRENT_SOURCE_DIR}/CMSIS_RTOS_V2
    ${CMAKE_CURRENT_SOURCE_DIR}/portable/GCC/ARM_CM4F
endif()