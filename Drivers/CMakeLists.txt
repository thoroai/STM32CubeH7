if(P32_BOOTCODE)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/CMSIS)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/STM32H7xx_HAL_Driver)
endif()

if(QSPI_EXTLOADER)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/CMSIS)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/STM32H7xx_HAL_Driver)
endif()

if(SC50_MMC)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/CMSIS)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/STM32H7xx_HAL_Driver)
endif()
