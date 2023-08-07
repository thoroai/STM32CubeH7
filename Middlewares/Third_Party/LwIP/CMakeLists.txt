if(${USING_LWIP} EQUAL 1)
    set(LWIP_SOURCES)
    list(APPEND LWIP_SOURCES
        ${CMAKE_CURRENT_SOURCE_DIR}/src/api/api_lib.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/api/api_msg.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/api/err.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/api/netbuf.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/api/netdb.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/api/netifapi.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/api/sockets.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/api/tcpip.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/apps/http/fs.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/apps/http/httpd.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/apps/lwiperf/lwiperf.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/ipv4/autoip.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/ipv4/dhcp.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/ipv4/etharp.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/ipv4/icmp.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/ipv4/igmp.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/ipv4/ip4.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/ipv4/ip4_addr.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/ipv4/ip4_frag.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/def.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/dns.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/inet_chksum.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/init.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/ip.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/mem.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/memp.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/netif.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/pbuf.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/raw.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/stats.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/sys.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/tcp.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/tcp_in.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/tcp_out.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/timeouts.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/core/udp.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/netif/ethernet.c
        
        )

        add_library(
            lwip_sources_appcode
            ${LWIP_SOURCES}
        )

        target_include_directories(
            lwip_sources_appcode
            PUBLIC
            ${CMAKE_CURRENT_SOURCE_DIR}/src/include
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