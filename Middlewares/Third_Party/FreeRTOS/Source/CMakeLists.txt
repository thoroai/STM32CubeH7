if(${USING_RTOS} EQUAL 1)
    set(ARM_CM     ARM_CM4F)
    add_library(
        freeRTOS_Source_appcode
        STATIC
        ${CMAKE_CURRENT_SOURCE_DIR}/
        croutine.c
        event_groups.c
        list.c
        queue.c
        stream_buffer.c
        tasks.c
        timers.c
        portable/MemMang/heap_4.c
        portable/GCC/${ARM_CM}/port.c
        CMSIS_RTOS_V2/cmsis_os2.c
    )

    target_include_directories(
        freeRTOS_Source_appcode
        PUBLIC
        ${CMAKE_SOURCE_DIR}/lib/stm32_cube_h7/Middlewares/Third_Party/FreeRTOS/Source/include
        ${CMAKE_SOURCE_DIR}/src/config/rtos/p32
        ${CMAKE_SOURCE_DIR}/lib/stm32_cube_h7/Drivers/CMSIS/Include
        ${CMAKE_SOURCE_DIR}/lib/stm32_cube_h7/Drivers/CMSIS/Device/ST/STM32H7xx/Include
        ${CMAKE_SOURCE_DIR}/lib/stm32_cube_h7/Drivers/STM32H7xx_HAL_Driver/Inc
        ${CMAKE_SOURCE_DIR}/src/config/hw/sc50_mmc
    )

    target_link_libraries(
        freeRTOS_Source_appcode
        PUBLIC
        cross_service_appcode
        GCC_ARM_CM4F
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

    if(${DEBUG} EQUAL 1)
    list(APPEND COMPILE_OPTS
        -g -gdwarf-2)
    endif()

    set(LINK_OPTS
        -mcpu=cortex-m7 #essential: will build but not flash without
        -T${CMAKE_SOURCE_DIR}/build/shared/stm32h7/stm32h750xbhx_flash.ld
        -mthumb
        -mfpu=fpv5-d16
        -specs=nano.specs
        -specs=nosys.specs
        -lc
        -lm
        -lnosys
        -Wl,-Map=p32_bootcode.map,--cref -Wl,--gc-sections
        -Wall
        -fdata-sections
        -ffunction-sections
        -w
    )

    if(${DEBUG} EQUAL 1)
        list(APPEND C_DEFS
            -DDEBUG)
    endif()

    # if(${USING_QSPI_TEST} EQUAL 1)
    # list(APPEND C_DEFS
    #     -DUSING_QSPI_TEST)
    # endif()

    if(${USING_DCACHE} EQUAL 1)
        list(APPEND C_DEFS
            -DUSING_DCACHE)
    endif()

    target_compile_definitions(
        freeRTOS_Source_appcode
        PUBLIC
        ${C_DEFS}
    )

    target_compile_options(
        freeRTOS_Source_appcode
        PUBLIC
        ${COMPILE_OPTS}
    )
        
    target_compile_options(
        freeRTOS_Source_appcode
        PUBLIC
    )
endif()