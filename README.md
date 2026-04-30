# Raspberry Pi Pico W Keypad-to-LED Controller

This project runs on a **Raspberry Pi Pico W (RP2040)** and maps key presses from a **4x4 membrane keypad** to **12 discrete LEDs**.

- Numeric keys `1..8` turn ON individual blue LEDs.
- Key `9` turns ON all blue LEDs (`1..8`).
- Key `0` turns OFF all blue LEDs (`1..8`).
- Keys `A..D` turn ON individual red LEDs.
- Key `*` turns ON all red LEDs (`A..D`).
- Key `#` turns OFF all red LEDs (`A..D`).

> Core behavior and key mapping are preserved from the provided firmware logic.

## Repository Structure

```text
.
├── CMakeLists.txt
├── include/
├── src/
│   └── main.cpp
└── docs/
    ├── architecture.md
    └── wiring.md
```

## Features

- 4x4 keypad scan using `Keypad` library
- 12 GPIO-controlled LED outputs
- Group ON/OFF controls for blue and red LED banks
- Simple cooperative loop with 10 ms poll delay

## Hardware Components

Derived from the supplied Wokwi `diagram.json`:

- 1x Raspberry Pi Pico / Pico W board
- 1x 4x4 membrane keypad
- 12x LEDs (8 blue + 4 red)
- 12x 220 Ω current-limiting resistors (LED series)
- 4x 1 kΩ resistors (keypad row pull-up network to 3.3V)
- Wiring + common GND rail

## Quick Start (Wokwi)

1. Open Wokwi and create a **Raspberry Pi Pico W** project.
2. Paste `src/main.cpp` firmware into the sketch source.
3. Use the provided `diagram.json` wiring.
4. Start simulation and press keypad buttons.

## Run on Real Hardware (Arduino-Pico toolchain)

Because the firmware is Arduino-style (`setup()/loop()` + `Keypad.h`), the simplest path is Arduino tooling.

1. Install Arduino IDE 2.x.
2. Install board package **Raspberry Pi Pico/RP2040 by Earle Philhower**.
3. Install library **Keypad** by Mark Stanley / Alexander Brevig.
4. Select board: **Raspberry Pi Pico W**.
5. Build and upload `src/main.cpp`.

## Optional: Pico SDK Users

A placeholder `CMakeLists.txt` is included to keep a C/C++-friendly repository layout. To build with Pico SDK directly, firmware must be ported from Arduino abstractions (`pinMode`, `digitalWrite`, `delay`, `Keypad`).

## Wi-Fi Notes

This firmware does **not** use Wi-Fi. No credentials are needed.

## Documentation

- Wiring and GPIO map: [`docs/wiring.md`](docs/wiring.md)
- Firmware architecture: [`docs/architecture.md`](docs/architecture.md)
