# SPDX-License-Identifier: Apache-2.0

cmake_minimum_required(VERSION 3.13.1)

include($ENV{ZEPHYR_BASE}/cmake/app/boilerplate.cmake NO_POLICY_SCOPE)
project(br_zephyr_ble)

FILE(GLOB app_sources src/*.c)
FILE(GLOB gatt_sources src/gatt/*.c)
target_sources(app PRIVATE
  ${app_sources}
  ${gatt_sources}
  )

# Files in these dirs can be included as system libs. Eg: <gatt/hrs.h>
# zephyr_library_include_directories($ENV{ZEPHYR_BASE}/samples/bluetooth)
