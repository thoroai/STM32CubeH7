

if(P32_BOOTCODE)
    add_subdirectory(FreeRTOS/Source/portable/GCC/ARM_CM4F)
    add_subdirectory(FreeRTOS/Source/include)
endif()

if(QSPI_EXTLOADER)
    add_subdirectory(FreeRTOS/Source/portable/GCC/ARM_CM4F)
    add_subdirectory(FreeRTOS/Source/include)
endif()

if(SC50_MMC)
    add_subdirectory(FreeRTOS/Source)
    add_subdirectory(FreeRTOS/Source/include)
    add_subdirectory(FreeRTOS/Source/portable/GCC/ARM_CM4F)
    add_subdirectory(FatFs)
    add_subdirectory(LwIP)
endif()