if(P32_BOOTCODE)
    add_subdirectory(CMSIS)
    add_subdirectory(STM32H7xx_HAL_Driver)
endif()

if(QSPI_EXTLOADER)
    add_subdirectory(CMSIS)
    add_subdirectory(STM32H7xx_HAL_Driver)
endif()

if(SC50_MMC)
    add_subdirectory(CMSIS)
    add_subdirectory(STM32H7xx_HAL_Driver)
endif()
