# This is free and unencumbered software released into the public domain.
#
# Anyone is free to copy, modify, publish, use, compile, sell, or
# distribute this software, either in source code form or as a compiled
# binary, for any purpose, commercial or non-commercial, and by any
# means.
#
# In jurisdictions that recognize copyright laws, the author or authors
# of this software dedicate any and all copyright interest in the
# software to the public domain. We make this dedication for the benefit
# of the public at large and to the detriment of our heirs and
# successors. We intend this dedication to be an overt act of
# relinquishment in perpetuity of all present and future rights to this
# software under copyright law.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
# EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
# MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
# IN NO EVENT SHALL THE AUTHORS BE LIABLE FOR ANY CLAIM, DAMAGES OR
# OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE,
# ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
# OTHER DEALINGS IN THE SOFTWARE.
#
# For more information, please refer to <http://unlicense.org/>

project(json)
cmake_minimum_required(VERSION 2.8.7)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../)

add_executable(json_test
  ../json.h
  ../json.c
  allocator.cpp
  allow_c_style_comments.cpp
  allow_equals_in_object.c
  allow_global_object.c
  allow_hexadecimal_numbers.c
  allow_inf_and_nan.c
  allow_json5.c
  allow_leading_or_trailing_decimal_point.c
  allow_leading_plus_sign.c
  allow_location_information.c
  allow_multi_line_strings.c
  allow_no_commas.c
  allow_single_quoted_strings.c
  allow_trailing_comma.cpp
  allow_unquoted_keys.c
  main.c
  test.c
  test.cpp
  write_minified.cpp
  write_pretty.cpp
)

if("${CMAKE_C_COMPILER_ID}" STREQUAL "GNU")
  set_source_files_properties(../json.c test.c test.cpp PROPERTIES
    COMPILE_FLAGS "-Wall -Wextra -Werror"
  )
elseif("${CMAKE_C_COMPILER_ID}" STREQUAL "Clang")
  set_source_files_properties(../json.c test.c test.cpp PROPERTIES
    COMPILE_FLAGS "-Wall -Wextra -Weverything -Werror"
  )
elseif("${CMAKE_C_COMPILER_ID}" STREQUAL "MSVC")
  set_source_files_properties(../json.c test.c test.cpp PROPERTIES
    COMPILE_FLAGS "/Wall /WX /wd4514"
  )
else()
  message(WARNING "Unknown compiler '${CMAKE_C_COMPILER_ID}'!")
endif()
