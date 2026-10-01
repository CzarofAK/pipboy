# Hardware

## Parts

| Part | Notes |
| --- | --- |
| ESP32 DevKit (ESP32-WROOM-32) | No PSRAM. Loose dev board, pins freely assignable |
| 2.8" TFT SPI module, ILI9341, 320×240, XPT2046 resistive touch | Same module type as used with the DIYBMS v4 controller (Stuart Pittaway) |
| Optional: NPN transistor or logic-level MOSFET + resistor | For PWM backlight dimming on GPIO25 |

## Wiring (ESP32 DevKit → 2.8" module)

Strapping pins (GPIO 0, 2, 5, 12, 15) are deliberately avoided. Display and touch
share the VSPI bus.

| Module pin | ESP32 | Notes |
| --- | --- | --- |
| VCC | 3V3 | When powered from 3.3 V, close solder jumper J1 on the module (bypasses the onboard regulator) |
| GND | GND | |
| CS | GPIO27 | |
| RESET | GPIO33 | |
| DC | GPIO26 | |
| SDI (MOSI) | GPIO23 | Shared with T_DIN |
| SCK | GPIO18 | Shared with T_CLK |
| LED | 3V3 (first test) | Later via NPN/MOSFET on GPIO25 for dimming |
| SDO (MISO) | GPIO19 | Shared with T_DO |
| T_CLK | GPIO18 | |
| T_CS | GPIO32 | |
| T_DIN | GPIO23 | |
| T_DO | GPIO19 | |
| T_IRQ | GPIO35 | Input-only pin, fine for IRQ |

## Bring-up

1. **Check the package path:** the config includes
   `github://czarofak/esphome_basics/basics.yaml@main`. Adjust file name or branch if
   they differ.
2. **Backlight:** while LED is tied directly to 3V3, comment out the `output:` and
   `light:` blocks.
3. **Flash** [`esphome/pipboy-display.yaml`](../esphome/pipboy-display.yaml). Expected
   result: black screen with green tabs STAT / INV / DATA / RADIO.
4. **Fix orientation and colours:**
   - Image upside down → `rotation: 270`
   - Colours inverted (white background) → `invert_colors: true`
5. **Calibrate touch:** tap the four corners and read `raw_x` / `raw_y` from the log.
   Enter the extremes as `x_min` / `x_max` / `y_min` / `y_max`. If touch is mirrored,
   toggle `mirror_x` / `mirror_y`.
6. **Afterwards** set the logger level from `DEBUG` back to `INFO`.

## Planned additions (desktop controller)

GPIOs still free on the WROOM DevKit after display and touch:

| GPIO | Type | Suggested use |
| --- | --- | --- |
| 4 | I/O | Piezo buzzer for the Geiger counter (LEDC, via NPN transistor) |
| 13, 14 | I/O | Rotary encoder 1 A/B (tab switching) |
| 16, 17 | I/O | Rotary encoder 2 A/B (scrolling) |
| 21, 22 | I/O | Push buttons (quick actions) – or I²C if an expander is needed later |
| 34, 36, 39 | Input only, no internal pull-ups | Encoder push switches / buttons with external pull-up resistors |

If more controls are needed than pins are available, use an I²C GPIO expander
(e.g. MCP23017) on GPIO21/22.

The pin assignment is a proposal and will be fixed once the controls are chosen.

## Known uncertainties

- The `tabview` widget syntax and the combination of display `rotation` with the touch
  `transform` have not yet been validated against the ESPHome version in use. If
  validation fails, adjust according to the error message.
- LVGL runs with a partial buffer (`buffer_size: 25%`) because the WROOM has no PSRAM.
