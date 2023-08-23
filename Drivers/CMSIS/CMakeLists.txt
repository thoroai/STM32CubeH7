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

    target_link_options(
        CMSIS_bootcode
        INTERFACE
        ${LINK_OPTS}
    )

    target_compile_definitions(
        CMSIS_bootcode
        INTERFACE
        ${C_DEFS}
    )
    
    add_subdirectory(RTOS2)
endif()

if(QSPI_EXTLOADER)
    add_subdirectory(RTOS2)
endif()

if(SC50_MMC)
    add_subdirectory(RTOS2)
endif()