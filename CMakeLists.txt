cmake_minimum_required(VERSION 3.13)
project(pico_w_keypad_led_controller C CXX)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# NOTE:
# This repository contains Arduino-style firmware in src/main.cpp.
# Build with Arduino-Pico (Earle Philhower) in Arduino IDE/PlatformIO,
# or adapt to Pico SDK entrypoints if required.
add_custom_target(firmware_source_only ALL
  COMMENT "Firmware source prepared for Arduino-Pico toolchain")
