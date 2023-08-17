

if(SC50_MMC)
    if(${USING_USB} EQUAL 1)
        add_library(
            stm32_usbhost_appcode
            STATIC
            core/src/usbh_ctlreq.c
            core/src/usbh_ioreq.c
            core/src/usbh_pipes.c
            class/msc/src/usbh_msc.c
            class/msc/src/usbh_msc_bot.c
            class/msc/src/usbh_msc_scsi.c

            # ${STM32_usb_HOST_MODIFIED}/usbh_core.c
            # ${STM32_usb_HOST_MODIFIED}/${TARGET}/usbh_platform.c
            # ${STM32_usb_HOST_MODIFIED}/usbh_conf.c
            )

    endif()
endif()