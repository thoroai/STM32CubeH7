message("FATFS DIR")

if(SC50_MMC)
    if(${USING_FATFS} EQUAL 1)
        add_library(
            fatfs_appcode
            ${CMAKE_CURRENT_SOURCE_DIR}/diskio.c
            ${CMAKE_CURRENT_SOURCE_DIR}/ff.c
            ${CMAKE_CURRENT_SOURCE_DIR}/ff_gen_drv.c
            ${CMAKE_CURRENT_SOURCE_DIR}/option/syscall.c
            ${CMAKE_CURRENT_SOURCE_DIR}/option/unicode.c
            )
    endif()
endif()