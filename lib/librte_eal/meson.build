# SPDX-License-Identifier: BSD-3-Clause
# Copyright(c) 2017-2019 Intel Corporation

# Custom EAL processing. EAL is complicated enough that it can't just
# have a straight list of headers and source files.
# Initially pull in common settings
eal_inc = [global_inc]
subdir('common') # defines common_sources, common_objs, etc.

# Now do OS/exec-env specific settings, including building kernel modules
# The <exec-env>/eal/meson.build file should define env_sources, etc.
if host_machine.system() == 'linux'
	dpdk_conf.set('RTE_EXEC_ENV_LINUX', 1)
	subdir('linux/eal')

elif host_machine.system() == 'freebsd'
	dpdk_conf.set('RTE_EXEC_ENV_FREEBSD', 1)
	subdir('freebsd/eal')

elif host_machine.system() == 'windows'
	dpdk_conf.set('RTE_EXEC_ENV_WINDOWS', 1)
	subdir('windows/eal')

else
	error('unsupported system type "@0@"'.format(host_machine.system()))
endif

version = 10  # the version of the EAL API
allow_experimental_apis = true
deps += 'kvargs'
if dpdk_conf.has('RTE_USE_LIBBSD')
	ext_deps += libbsd
endif
sources = common_sources + env_sources
objs = common_objs + env_objs
headers = common_headers + env_headers
includes = eal_inc
