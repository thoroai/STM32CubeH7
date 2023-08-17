
##################################
######### P32_BOOTCODE
##################################
if(P32_BOOTCODE)
    add_library(
        STM32H7xx_HAL_bootcode
        STATIC
        Src/stm32h7xx_hal_rcc.c 
        Src/stm32h7xx_hal_rcc_ex.c 
        Src/stm32h7xx_ll_rcc.c 
        Src/stm32h7xx_hal_gpio.c 
        Src/stm32h7xx_hal_dma.c 
        Src/stm32h7xx_hal_dma_ex.c 
        Src/stm32h7xx_hal_pwr.c 
        Src/stm32h7xx_hal_pwr_ex.c 
        Src/stm32h7xx_hal_cortex.c 
        Src/stm32h7xx_hal.c 
        Src/stm32h7xx_hal_qspi.c 
        Src/stm32h7xx_hal_spi.c 
        Src/stm32h7xx_hal_spi_ex.c 
        Src/stm32h7xx_hal_tim.c 
        Src/stm32h7xx_hal_tim_ex.c 
        Src/stm32h7xx_hal_hash.c 
        Src/stm32h7xx_hal_hash_ex.c
        Src/stm32h7xx_hal_mdma.c #might not need this?
    )
    
    target_include_directories(
        STM32H7xx_HAL_bootcode
        PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/Inc
        ${CMAKE_SOURCE_DIR}/src/config/hw/p32_bootcode  
        ${CMAKE_SOURCE_DIR}lib/customization/stm32_customizations
        ${CMAKE_SOURCE_DIR}/lib/customization/stm32_customizations/bootcode_conf
        ${CMAKE_SOURCE_DIR}/lib/customization/stm32_customizations/p32
    )

    target_link_libraries(
        STM32H7xx_HAL_bootcode
        PUBLIC
        CMSIS_bootcode
        hal_conf_bootcode
        stm32_customizations_bootcode
        # stm32_customizations_p32
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

    target_compile_definitions(
        STM32H7xx_HAL_bootcode 
        PUBLIC
        -DSTM32H750xx
    )

    target_compile_options(
        STM32H7xx_HAL_bootcode 
        PUBLIC 
        ${COMPILE_OPTS}
    )
    target_link_options(
        STM32H7xx_HAL_bootcode
        PUBLIC
        ${LINK_OPTS}
    )
endif()


##################################
######### QSPI_EXTLOADER
##################################
if(QSPI_EXTLOADER)
    add_library(
        STM32H7xx_HAL_extloader
        STATIC
        Src/stm32h7xx_hal.c
        Src/stm32h7xx_hal_cortex.c
        Src/stm32h7xx_hal_gpio.c
        Src/stm32h7xx_hal_pwr.c
        Src/stm32h7xx_hal_pwr_ex.c
        Src/stm32h7xx_hal_qspi.c
        Src/stm32h7xx_hal_rcc.c
        Src/stm32h7xx_hal_rcc_ex.c
        Src/stm32h7xx_hal_tim.c
        Src/stm32h7xx_hal_tim_ex.c
        Src/stm32h7xx_hal_mdma.c
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

    target_compile_definitions(
        STM32H7xx_HAL_extloader 
        PUBLIC 
        -DSTM32H750xx
    )

    target_compile_options(
        STM32H7xx_HAL_extloader 
        PUBLIC 
        ${COMPILE_OPTS}
    )
endif()

##################################
######### SC50_MMC
##################################
if(SC50_MMC)
    set(HAL_APP_SOURCES)

    list(APPEND HAL_APP_SOURCES
        Src/stm32h7xx_hal_hcd.c
    )

    if(${USING_ADC} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            Src/stm32h7xx_hal_adc.c
            Src/stm32h7xx_hal_adc_ex.c)
    endif()

    if(${USING_CRC} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            Src/stm32h7xx_hal_crc.c
            Src/stm32h7xx_hal_crc_ex.c)
    endif()

    if(${USING_DAC} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            Src/stm32h7xx_hal_dac.c
            Src/stm32h7xx_hal_dac_ex.c)
    endif()

    list(APPEND HAL_APP_SOURCES
        Src/stm32h7xx_hal_rcc.c
        Src/stm32h7xx_hal_rcc_ex.c
        Src/stm32h7xx_ll_rcc.c
        Src/stm32h7xx_hal_gpio.c
        Src/stm32h7xx_hal_dma.c
        Src/stm32h7xx_hal_dma_ex.c
        Src/stm32h7xx_hal_pwr.c
        Src/stm32h7xx_hal_pwr_ex.c
        Src/stm32h7xx_hal_cortex.c
        Src/stm32h7xx_hal.c
        Src/stm32h7xx_hal_i2c.c
        Src/stm32h7xx_hal_i2c_ex.c
        Src/stm32h7xx_hal_exti.c
        Src/stm32h7xx_hal_iwdg.c)

    if(${USING_DISPLAY} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            Src/stm32h7xx_hal_ltdc.c)
    endif()

    if(${USING_TOUCHGFX} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            Src/stm32h7xx_hal_dma2d.c)
    endif()

    if(${USING_CAN} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            Src/stm32h7xx_hal_fdcan.c)
    endif()

    if(${USING_QSPI} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            Src/stm32h7xx_hal_qspi.c)
    endif()

    if(${USING_FLASH} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            Src/stm32h7xx_hal_flash.c
            Src/stm32h7xx_hal_flash_ex.c)
    endif()

    if(${USING_FMC} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            Src/${STM32_LL}_fmc.c
            Src/stm32h7xx_hal_sdram.c)
    endif()

    list(APPEND HAL_APP_SOURCES
        Src/stm32h7xx_hal_rtc.c
        Src/stm32h7xx_hal_rtc_ex.c
        Src/stm32h7xx_hal_spi.c
        Src/stm32h7xx_hal_spi_ex.c
        Src/stm32h7xx_hal_tim.c
        Src/stm32h7xx_hal_tim_ex.c)

    if(${USING_UART} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            Src/stm32h7xx_hal_uart.c
            Src/stm32h7xx_hal_uart_ex.c
            Src/stm32h7xx_ll_usart.c
            )
    endif()

    if(${USING_HASH} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            Src/stm32h7xx_hal_hash.c
            Src/stm32h7xx_hal_hash_ex.c)
    endif()

    if(${USING_EMMC} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            Src/stm32h7xx_hal_sdmmc.c
            Src/stm32h7xx_hal_mmc.c
            Src/stm32h7xx_hal_mmc_ex.c)
    endif()

    if(${USING_USB} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            Src/stm32h7xx_hal_usb.c
            )
    endif()

    if(${USING_LWIP} EQUAL 1)
        list(APPEND HAL_APP_SOURCES
            Src/stm32h7xx_hal_eth.c)
    endif()

    add_library(
        STM32H7xx_HAL_appcode
        STATIC
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
        cross_service_appcode
        p32_customized_appcode
    )

    target_compile_definitions(
        STM32H7xx_HAL_appcode
        PUBLIC
        ${C_DEFS}
    )

    set(COMPILE_OPTS
        ${C_DEFS}
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

    target_link_options(
        STM32H7xx_HAL_appcode
        PUBLIC
        ${SC50_LDFLAGS}
        # -Map=${CMAKE_SOURCE_DIR}/sc50_appcode.map
    )

endif()