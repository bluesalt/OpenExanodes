#
# Copyright 2002, 2009 Seanodes Ltd http://www.seanodes.com. All rights
# reserved and protected by French, UK, U.S. and other countries' copyright laws.
# This file is part of Exanodes project and is subject to the terms
# and conditions defined in the LICENSE file which is present in the root
# directory of the project.
#

add_library(service_rdev STATIC
	service_rdev.c
	rdev_config.c
        broken_disk_table.c)

target_link_libraries(service_rdev
        rdev
	exa_common_user)

