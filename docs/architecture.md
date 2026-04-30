# Firmware Architecture

## 1) High-Level Design

The firmware is a single-module event loop:
1. Initialize all LED GPIOs as outputs and drive LOW.
2. Poll keypad state continuously.
3. When a key is pressed, execute fixed LED control actions.

No interrupts, RTOS tasks, or dynamic memory are used.

## 2) Source Layout

- `src/main.cpp`
  - Declares keypad matrix map (`keys[4][4]`)
  - Declares LED GPIO map (`ledPins[12]`)
  - Declares row/column GPIO maps
  - Initializes `Keypad` object
  - Implements `setup()` and `loop()`

## 3) Data Structures

- `keys[ROWS][COLS]`: Key symbol matrix used by the Keypad library.
- `ledPins[LEDS]`: Index-based LED GPIO map:
  - indexes `0..7` for keys `1..8`
  - indexes `8..11` for keys `A..D`
- `rowPins` / `colPins`: Keypad wiring declaration.

## 4) Control Flow

### setup()
- Iterate over all 12 LED pins:
  - `pinMode(pin, OUTPUT)`
  - `digitalWrite(pin, LOW)`

### loop()
- Read one key using `keypad.getKey()`.
- If a valid key exists, dispatch through `switch (key)`.
- Execute single LED action or grouped for-loops (`9`, `0`, `*`, `#`).
- Delay 10 ms to limit polling rate.

## 5) Behavioral Notes

- Press actions are one-shot on key detection.
- There is no explicit toggle/off for single LEDs except group-off keys (`0`, `#`) or reset.
- Logic is deterministic and directly tied to fixed key mappings.

## 6) Portability Notes

Current code targets Arduino APIs and the `Keypad` library. A pure Pico SDK version would require replacing:
- GPIO calls (`pinMode`, `digitalWrite`)
- Timing (`delay`)
- Keypad scanning implementation/library
