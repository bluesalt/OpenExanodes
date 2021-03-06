#
# Copyright 2002, 2009 Seanodes Ltd http://www.seanodes.com. All rights
# reserved and protected by French, UK, U.S. and other countries' copyright laws.
# This file is part of Exanodes project and is subject to the terms
# and conditions defined in the LICENSE file which is present in the root
# directory of the project.
#

if (NOT WIN32)
    set(LINUX_SOURCES
        exa_socket.c
        exa_thread_name.c)
endif (NOT WIN32)

add_library(exa_common_user STATIC
    ${LINUX_SOURCES}
    checksum.c
    threadonize.c
    exa_conversion.c
    exa_error.c
    exa_nodeset.c
    exa_select.c
    exa_system.c
    exa_names.c
    exa_env.c
    exa_version.c
    uuid.c
    ${MEMTRACE_SOURCES})

target_link_libraries(exa_common_user exa_os)

if (NOT WIN32)
    set_target_properties(exa_common_user PROPERTIES COMPILE_FLAGS "-fPIC")
endif (NOT WIN32)

add_library(daemon_lightclient
    daemon_api_lightclient.c)

add_library(daemon_server
    daemon_api_server.c)

add_library(daemon_request_queue
    daemon_request_queue.c)

add_library(exa_config
    exa_config.c)

target_link_libraries(exa_config
    ${LIBXML2_LIBRARIES})

add_library(exa_nbd_list STATIC exa_nbd_list.c)

target_link_libraries(exa_nbd_list exa_os)

# --- kernel module --------------------------------------------

if (WITH_NODES AND NOT WIN32)

    include(KernelModule)

    add_kernel_module(exa_common
        exa_common_kernel.c
        exa_select_kernel.c
        exa_socket_kernel.c
        exa_thread_name_kernel.c
        exa_common_kernel.h
        exa_select_kernel.h
        exa_socket_kernel.h
        exa_thread_name_kernel.h)

endif (WITH_NODES AND NOT WIN32)

