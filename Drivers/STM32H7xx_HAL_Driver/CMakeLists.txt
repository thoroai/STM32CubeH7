
# create shared lib first that has all sources that are used across all builds:boot, qspi, app


if(P32_BOOTCODE ON)
    add_library(
        STM32H7xx_HAL_bootcode
        SHARED
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_rcc.c 
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_rcc_ex.c 
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_ll_rcc.c 
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_gpio.c 
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_dma.c 
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_dma_ex.c 
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_pwr.c 
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_pwr_ex.c 
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_cortex.c 
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal.c 
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_qspi.c 
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_spi.c 
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_spi_ex.c 
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_tim.c 
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_tim_ex.c 
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_hash.c 
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_hash_ex.c
    )
    
    target_include_directories(
        STM32H7xx_HAL_bootcode
        ${CMAKE_CURRENT_SOURCE_DIR}/Inc
    )
endif()

#libraries for qspi
if(QSPI_EXTLOADER ON)
endif()

#libraries for sc50-appcode
if(SC50_MMC_APPCODE ON)
endif()