# target_include_directories(${CMAKE_CURRENT_SOURCE_DIR})

# add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/BSP)
# add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/CMSIS)


if(P32_BOOTCODE)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/STM32H7xx_HAL_Driver)
endif()

if(QSPI_EXTLOADER)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/CMSIS)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/STM32H7xx_HAL_Driver)
endif()