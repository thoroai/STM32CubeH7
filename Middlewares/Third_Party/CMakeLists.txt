

if(P32_BOOTCODE)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS/Source/portable/GCC/ARM_CM4F)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS/Source/include)
endif()

if(QSPI_EXTLOADER)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS/Source/portable/GCC/ARM_CM4F)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS/Source/include)
endif()

if(SC50_MMC)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS/Source)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS/Source/include)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS/Source/portable/GCC/ARM_CM4F)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/FatFs)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/LwIP)
endif()