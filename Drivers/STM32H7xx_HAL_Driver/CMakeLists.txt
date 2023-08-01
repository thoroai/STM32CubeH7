
# create shared lib first that has all sources that are used across all builds:boot, qspi, app


if(P32_BOOTCODE)
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
        PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/Inc
        ${CMAKE_SOURCE_DIR}/src/config/hw/p32_bootcode  
        ${CMAKE_SOURCE_DIR}lib/customization/stm32_customizations
    )

    target_link_libraries(
        STM32H7xx_HAL_bootcode
        PUBLIC
        CMSIS_bootcode
        hal_conf_bootcode
    )

    ######################################
    # Compiler Options
    ######################################
    set(COMPILE_OPTS 
    -mcpu=cortex-m7
    -mthumb
    -mfpu=fpv5-d16
    -mfloat-abi=softfp
    -fdata-sections
    -ffunction-sections
    -Wall
    -MMD
    -MP
    -w
    $<$<CONFIG:Debug>:-Og>)

    target_compile_definitions(STM32H7xx_HAL_bootcode PUBLIC -DSTM32H750xx)
    target_compile_options(STM32H7xx_HAL_bootcode PUBLIC ${COMPILE_OPTS})
endif()


############################################## QSPI ########################################################
#libraries for qspi
if(QSPI_EXTLOADER)
    add_library(
        STM32H7xx_HAL_qspi_loader
        SHARED
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_cortex.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_gpio.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_pwr.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_pwr_ex.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_qspi.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_rcc.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_rcc_ex.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_tim.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_tim_ex.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_mdma.c
    )

    target_include_directories(
        STM32H7xx_HAL_bootcode
        ${CMAKE_CURRENT_SOURCE_DIR}/Inc
    )
endif()

#libraries for sc50-appcode
if(SC50_MMC_APPCODE)
endif()