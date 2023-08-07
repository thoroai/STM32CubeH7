# target_include_directories(${CMAKE_CURRENT_SOURCE_DIR})

if(P32_BOOTCODE)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/Drivers)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/Middlewares)
endif()

if(QSPI_EXTLOADER)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/Drivers)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/Middlewares)
endif()

if(SC50_MMC)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/Middlewares)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/Drivers)
endif()