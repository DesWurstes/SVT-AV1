#
# Copyright(c) 2019 Intel Corporation
# SPDX - License - Identifier: BSD - 2 - Clause - Patent
#

# Libraries Directory CMakeLists.txt

function(test_apply_compiler_flags flags current_flags)
    foreach(cflag ${${flags}})
        string(REGEX REPLACE "[^A-Za-z0-9]" "_" cflag_var "${cflag}")
        set(test_c_flag "C_FLAG${cflag_var}")
        check_c_compiler_flag(${cflag} "${test_c_flag}")
        if(${test_c_flag})
            set(${current_flags} "${${current_flags}} ${cflag}" PARENT_SCOPE)
        endif()
    endforeach()
endfunction()

add_subdirectory(Codec)
add_subdirectory(C_DEFAULT)
add_subdirectory(ASM_SSE2)
add_subdirectory(ASM_SSSE3)
add_subdirectory(ASM_SSE4_1)
add_subdirectory(ASM_AVX2)
