

if(SC50_MMC)
    if(${USING_USB} EQUAL 1)
        add_library(
            stm32_usbhost_appcode
            ${CMAKE_CURRENT_SOURCE_DIR}/core/src/usbh_ctlreq.c
            ${CMAKE_CURRENT_SOURCE_DIR}/core/src/usbh_ioreq.c
            ${CMAKE_CURRENT_SOURCE_DIR}/core/src/usbh_pipes.c
            ${CMAKE_CURRENT_SOURCE_DIR}/class/msc/src/usbh_msc.c
            ${CMAKE_CURRENT_SOURCE_DIR}/class/msc/src/usbh_msc_bot.c
            ${CMAKE_CURRENT_SOURCE_DIR}/class/msc/src/usbh_msc_scsi.c

            # ${STM32_usb_HOST_MODIFIED}/usbh_core.c
            # ${STM32_usb_HOST_MODIFIED}/${TARGET}/usbh_platform.c
            # ${STM32_usb_HOST_MODIFIED}/usbh_conf.c
            )

    endif()
endif()