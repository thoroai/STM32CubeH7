# target_include_directories(${CMAKE_CURRENT_SOURCE_DIR})

if(P32_BOOTCODE)
    add_subdirectory(Drivers)
    add_subdirectory(Middlewares)
endif()

if(QSPI_EXTLOADER)
    add_subdirectory(Drivers)
    add_subdirectory(Middlewares)
endif()

if(SC50_MMC)
    add_subdirectory(Middlewares)
    add_subdirectory(Drivers)
endif()