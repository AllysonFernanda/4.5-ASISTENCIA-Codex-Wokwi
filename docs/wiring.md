# Wiring and GPIO Mapping (Raspberry Pi Pico W)

## 1) Overview

The circuit contains:
- 4x4 membrane keypad connected as 4 row lines + 4 column lines.
- 12 LEDs driven by GPIO through 220 Ω resistors.
- Common cathode return to GND for all LEDs.
- A 1 kΩ pull-up chain from 3V3 feeding keypad row lines (as drawn in the provided diagram).

## 2) Keypad Connections

| Keypad Pin | Pico W GPIO |
|---|---|
| C1 | GP19 |
| C2 | GP18 |
| C3 | GP17 |
| C4 | GP16 |
| R1 | GP26 |
| R2 | GP22 |
| R3 | GP21 |
| R4 | GP20 |

Pull-up network in diagram:
- R1/R2/R3/R4 keypad row lines are also tied via 1 kΩ resistors to a 3V3 rail.

## 3) LED Connections

All LEDs are active-HIGH in firmware (`digitalWrite(pin, HIGH)` turns LED ON).
Each LED anode is connected to a GPIO through a 220 Ω resistor; each cathode goes to GND.

| Logical LED | Key Trigger | Pico W GPIO |
|---|---|---|
| LED1 | `1` | GP11 |
| LED2 | `2` | GP10 |
| LED3 | `3` | GP9 |
| LED4 | `4` | GP8 |
| LED5 | `5` | GP7 |
| LED6 | `6` | GP6 |
| LED7 | `7` | GP5 |
| LED8 | `8` | GP4 |
| LED9 (A) | `A` | GP3 |
| LED10 (B) | `B` | GP2 |
| LED11 (C) | `C` | GP28 |
| LED12 (D) | `D` | GP27 |

## 4) Group Actions

- `9`: turns ON LED1..LED8 (blue bank)
- `0`: turns OFF LED1..LED8
- `*`: turns ON LED9..LED12 (red bank)
- `#`: turns OFF LED9..LED12

## 5) Assumptions / Clarifications

- The provided firmware pin arrays are treated as authoritative for behavior.
- Diagram LED labels (1..8, A..D) align with key semantics, though physical left-right placement may differ.
- Pico and Pico W share the same exposed GPIO mapping for this use case.
