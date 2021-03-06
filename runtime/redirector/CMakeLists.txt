################################################################################
# Copyright (c) 2017, 2018 IBM Corp. and others
#
# This program and the accompanying materials are made available under
# the terms of the Eclipse Public License 2.0 which accompanies this
# distribution and is available at https://www.eclipse.org/legal/epl-2.0/
# or the Apache License, Version 2.0 which accompanies this distribution and
# is available at https://www.apache.org/licenses/LICENSE-2.0.
#
# This Source Code may also be made available under the following
# Secondary Licenses when the conditions for such availability set
# forth in the Eclipse Public License, v. 2.0 are satisfied: GNU
# General Public License, version 2 with the GNU Classpath
# Exception [1] and GNU General Public License, version 2 with the
# OpenJDK Assembly Exception [2].
#
# [1] https://www.gnu.org/software/classpath/license.html
# [2] http://openjdk.java.net/legal/assembly-exception.html
#
# SPDX-License-Identifier: EPL-2.0 OR Apache-2.0 OR GPL-2.0 WITH Classpath-exception-2.0 OR LicenseRef-GPL-2.0 WITH Assembly-exception
################################################################################

# Don't append version suffix.
set(CMAKE_SHARED_LIBRARY_SUFFIX ${J9VM_OLD_SHARED_SUFFIX})

set_source_files_properties("${CMAKE_CURRENT_BINARY_DIR}/generated.c" PROPERTIES GENERATED TRUE)

################################################################################
# Redirector
################################################################################
add_library(jvm_redirect SHARED
	"${CMAKE_CURRENT_BINARY_DIR}/generated.c"
	redirector.c
)
target_link_libraries(jvm_redirect
	PRIVATE
		j9vm_interface
		dl
)
target_include_directories(jvm_redirect
	PRIVATE
		"${j9vm_SOURCE_DIR}/j9vm"
		"${j9vm_BINARY_DIR}/j9vm"
)
set_target_properties(jvm_redirect PROPERTIES LIBRARY_OUTPUT_NAME jvm)

################################################################################
# Redirector b150
################################################################################
add_library(jvm_b150_redirect SHARED
	"${CMAKE_CURRENT_BINARY_DIR}/generated.c"
	redirector.c
)
target_link_libraries(jvm_b150_redirect
	PRIVATE
		j9vm_interface
		dl
)
target_include_directories(jvm_b150_redirect
	PRIVATE
		"${j9vm_SOURCE_DIR}/j9vm"
		"${j9vm_BINARY_DIR}/j9vm"
)
set_target_properties(jvm_b150_redirect PROPERTIES LIBRARY_OUTPUT_NAME jvm_b150)

################################################################################
# Redirector b156
################################################################################
add_library(jvm_b156_redirect SHARED
	"${CMAKE_CURRENT_BINARY_DIR}/generated.c"
	redirector.c
)
target_link_libraries(jvm_b156_redirect
	PRIVATE
		j9vm_interface
		dl
)
target_include_directories(jvm_b156_redirect
	PRIVATE
		"${j9vm_SOURCE_DIR}/j9vm"
		"${j9vm_BINARY_DIR}/j9vm"
)
set_target_properties(jvm_b156_redirect PROPERTIES LIBRARY_OUTPUT_NAME jvm_b156)

install(
	TARGETS jvm_b150_redirect jvm_b156_redirect jvm_redirect
	LIBRARY DESTINATION ${j9vm_SOURCE_DIR}/redirector
)
