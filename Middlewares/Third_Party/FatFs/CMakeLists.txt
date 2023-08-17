
if(SC50_MMC)
    if(${USING_FATFS} EQUAL 1)
        add_library(
            fatfs_appcode
            OBJECT
            src/diskio.c
            src/ff.c
            src/ff_gen_drv.c
            src/option/syscall.c
            src/option/unicode.c
            )

        target_include_directories(
            fatfs_appcode
            PUBLIC
            src
        )
    endif()
endif()