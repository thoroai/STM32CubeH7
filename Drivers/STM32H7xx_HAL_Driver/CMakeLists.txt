
##################################
######### P32_BOOTCODE
##################################
if(P32_BOOTCODE)
    add_library(
        STM32H7xx_HAL_bootcode
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

        ${CMAKE_CURRENT_SOURCE_DIR}/Src/stm32h7xx_hal_mdma.c #might not need this?
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
        stm32_customizations_bootcode
    )

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


##################################
######### QSPI_EXTLOADER
##################################
if(QSPI_EXTLOADER)
    message("BUILDING HAL FOR QSPI")
    add_library(
        STM32H7xx_HAL_extloader
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
        STM32H7xx_HAL_extloader
        PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/Inc
        ${CMAKE_SOURCE_DIR}/src/config/hw/extloader
        ${CMAKE_SOURCE_DIR}/lib/stm32_cube_h7/Drivers/CMSIS/Device/ST/STM32H7xx/Include
        ${CMAKE_SOURCE_DIR}/lib/stm32_cube_h7/Drivers/CMSIS/Include
    )

    target_link_libraries(
        STM32H7xx_HAL_extloader 
        PUBLIC
        hw_extloader
        stm_customizations_extloader
        )
    
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
        $<$<CONFIG:Debug>:-Og>
        )

    target_compile_definitions(STM32H7xx_HAL_extloader PUBLIC -DSTM32H750xx)
    target_compile_options(STM32H7xx_HAL_extloader PUBLIC ${COMPILE_OPTS})
endif()

##################################
######### SC50_MMC
##################################
if(SC50_MMC)
    set(HAL_APP_SOURCES)
    set(STM32_HAL  stm32h7xx_hal)


    list(APPEND HAL_APP_SOURCES
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_hcd.c
    )


    if(${USING_ADC} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_adc.c
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_adc_ex.c)
    endif()

    if(${USING_CRC} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_crc.c
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_crc_ex.c)
    endif()

    if(${USING_DAC} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_dac.c
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_dac_ex.c)
    endif()

    list(APPEND HAL_APP_SOURCES
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_rcc.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_rcc_ex.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_rcc.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_gpio.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_dma.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_dma_ex.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_pwr.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_pwr_ex.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_cortex.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_i2c.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_i2c_ex.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_exti.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_iwdg.c)

    if(${USING_DISPLAY} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_ltdc.c)
    endif()

    if(${USING_TOUCHGFX} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_dma2d.c)
    endif()

    if(${USING_CAN} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_fdcan.c)
    endif()

    if(${USING_QSPI} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_qspi.c)
    endif()

    if(${USING_FLASH} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_flash.c
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_flash_ex.c)
    endif()

    if(${USING_FMC} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_LL}_fmc.c
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_sdram.c)
    endif()

    list(APPEND HAL_APP_SOURCES
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_rtc.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_rtc_ex.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_spi.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_spi_ex.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_tim.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_tim_ex.c)

    if(${USING_UART} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_uart.c
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_uart_ex.c
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_usart.c)
    endif()

    if(${USING_HASH} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_hash.c
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_hash_ex.c)
    endif()

    if(${USING_EMMC} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_sdmmc.c
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_mmc.c
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_mmc_ex.c)
    endif()

    if(${USING_USB} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_usb.c
            )
    endif()

    if(${USING_LWIP} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            ${CMAKE_CURRENT_SOURCE_DIR}/Src/${STM32_HAL}_eth.c)
    endif()

    add_library(
        STM32H7xx_HAL_appcode
        ${HAL_APP_SOURCES}
    )

    target_include_directories(
        STM32H7xx_HAL_appcode
        PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/Inc
        ${CMAKE_SOURCE_DIR}/src/config/hw/sc50_mmc
        ${CMAKE_SOURCE_DIR}/lib/stm32_cube_h7/Drivers/CMSIS/Device/ST/STM32H7xx/Include
        ${CMAKE_SOURCE_DIR}/lib/stm32_cube_h7/Drivers/CMSIS/Include
    )

    target_link_libraries(
        STM32H7xx_HAL_appcode 
        PUBLIC
        )

    
    set(COMPILE_DEFS
        -DSTM32H7
        -DUSE_HAL_DRIVER
        -DSTM32H750xx
        -DEVENT_TRACE=${EVENT_TRACE_OPTION}
        "-D__FILENAME__=\"$(notdir $<)\""
        # ${C_DEFS}
        )

    target_compile_definitions(
        STM32H7xx_HAL_appcode
        PUBLIC
        ${COMPILE_DEFS}
    )

    set(COMPILE_OPTS
        ${COMPILE_DEFS}
        # ${C_INCLUDES}
        -mcpu=cortex-m7
        -mthumb
        -mfpu=fpv5-d16
        -mfloat-abi=softfp
        -fdata-sections
        -ffunction-sections
        -g3
        -fstack-usage
        -Wall
        -MMD
        -MP
        -std=gnu11
        -c
        -w
        $<$<CONFIG:Debug>:-Og>
        # -Wa,-a,-ad
        -O0
        )
    target_compile_options(
        STM32H7xx_HAL_appcode
        PUBLIC
        ${COMPILE_OPTS}
        )

endif()