

if(P32_BOOTCODE)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS/Source/portable/GCC/ARM_CM4F)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS/Source/include)
endif()

if(QSPI_EXTLOADER)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS/Source/portable/GCC/ARM_CM4F)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS/Source/include)
endif()