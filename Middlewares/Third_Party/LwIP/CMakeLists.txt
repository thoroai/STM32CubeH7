if(${USING_LWIP} EQUAL 1)
    set(LWIP_SOURCES)
    list(APPEND LWIP_SOURCES
        src/api/api_lib.c
        src/api/api_msg.c
        src/api/err.c
        src/api/netbuf.c
        src/api/netdb.c
        src/api/netifapi.c
        src/api/sockets.c
        src/api/tcpip.c
        src/apps/http/fs.c
        src/apps/http/httpd.c
        src/apps/lwiperf/lwiperf.c
        src/core/ipv4/autoip.c
        src/core/ipv4/dhcp.c
        src/core/ipv4/etharp.c
        src/core/ipv4/icmp.c
        src/core/ipv4/igmp.c
        src/core/ipv4/ip4.c
        src/core/ipv4/ip4_addr.c
        src/core/ipv4/ip4_frag.c
        src/core/def.c
        src/core/dns.c
        src/core/inet_chksum.c
        src/core/init.c
        src/core/ip.c
        src/core/mem.c
        src/core/memp.c
        src/core/netif.c
        src/core/pbuf.c
        src/core/raw.c
        src/core/stats.c
        src/core/sys.c
        src/core/tcp.c
        src/core/tcp_in.c
        src/core/tcp_out.c
        src/core/timeouts.c
        src/core/udp.c
        src/netif/ethernet.c
        
        )

        add_library(
            lwip_sources_appcode
            STATIC
            ${LWIP_SOURCES}
        )

        target_include_directories(
            lwip_sources_appcode
            PUBLIC
            src/include
            ${CMAKE_SOURCE_DIR}/src/config/ip/sc50_mmc
            ${CMAKE_SOURCE_DIR}/lib/customization/lwip
            ${CMAKE_SOURCE_DIR}/lib/stm32_cube_h7/Middlewares/Third_Party/FreeRTOS/Source/CMSIS_RTOS_V2
            ${CMAKE_SOURCE_DIR}/src/config/rtos/p32
        )

        target_link_libraries(
            lwip_sources_appcode
            PUBLIC
            freeRTOS_includes
            cross_service_appcode
            GCC_ARM_CM4F
        )
endif()