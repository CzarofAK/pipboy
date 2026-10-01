# Pip-Boy Touch Display for Fallout 4

A small, standalone Pip-Boy-style touch display for Fallout 4 on PC. It shows live
character data (HP, AP, radiation, carry weight, active quest, radio) and offers
quick actions (Stimpak, RadAway, radio off) without opening the in-game Pip-Boy.

## Architecture

```
Fallout 4 (PC)  ──Pip-Boy Companion protocol──▶  Bridge (Python, PyPipboy)  ──MQTT──▶  ESP32 + 2.8" touch display (ESPHome + LVGL)
     ▲                                                     │                                       │
     └──────────────── commands (use item, radio) ◀────────┴──────── MQTT commands ◀───────────────┘
```

- **Game side:** Fallout 4 still contains the Pip-Boy Companion App server. It is
  enabled in-game under *Settings → Gameplay → Pip-Boy App*.
- **Bridge:** a small Python script on the gaming PC. It uses the reverse-engineered
  protocol via [PyPipboy](https://github.com/matzman666/PyPipboy), publishes selected
  values to MQTT and forwards commands from MQTT back to the game.
- **Display:** an ESP32 DevKit (WROOM, no PSRAM) with a 2.8" ILI9341 / XPT2046 SPI
  touch module, running ESPHome with LVGL. Only the values that are displayed are
  kept on the device; the full Pip-Boy database stays on the bridge.

Why a bridge instead of parsing the protocol on the ESP32: the protocol sends a large
binary database on connect, which a WROOM without PSRAM cannot hold. The bridge also
keeps the display hardware interchangeable (e.g. a larger ESP32-P4 panel later).

The device is a **desktop controller** that sits next to the keyboard – not a
wrist-worn Pip-Boy replica. It combines the touch display with physical hardware
controls (e.g. rotary encoders and buttons).

## Repository layout

| Path | Content |
| --- | --- |
| [`esphome/pipboy-display.yaml`](esphome/pipboy-display.yaml) | ESPHome config: display, touch, Pip-Boy style LVGL layout (step 1, placeholders) |
| [`docs/hardware.md`](docs/hardware.md) | Hardware, wiring, bring-up and touch calibration |
| [`docs/protocol.md`](docs/protocol.md) | What is known about the Pip-Boy Companion protocol, existing libraries, connection test |
| [`bridge/`](bridge/) | PyPipboy → MQTT bridge (step 2, not written yet) |
| [`docs/fallout4-mod-setup.md`](docs/fallout4-mod-setup.md) | Mod setup guide used alongside this project (settlement building, 21:9 ultrawide, graphics) |

## Status / roadmap

- [x] Concept and architecture
- [x] Step 1: ESPHome display/touch config with Pip-Boy layout (untested on hardware)
- [ ] Wire up hardware, flash, fix rotation/colours, calibrate touch
- [ ] Protocol test: check that the game still answers the Companion protocol (see [`docs/protocol.md`](docs/protocol.md))
- [ ] Step 2: bridge (PyPipboy → MQTT) and MQTT topics
- [ ] Step 3: bind live values and buttons in ESPHome

## Planned features

| Feature | Description | Depends on |
| --- | --- | --- |
| Settlement alerts | Bridge watches workshop data (population, happiness, defense) and raises an alert on the display when a settlement is under attack or happiness drops below a threshold | Bridge, protocol test (workshop data available?) |
| Geiger counter | Piezo buzzer on the ESP32 clicks faster as radiation rises | Bridge (`pipboy/player/rad`), buzzer hardware |
| Compass strip | Narrow compass bar at the top of the display, showing heading and direction to the active quest target | Bridge (player position/heading, quest marker) |
| Hardware controls | Physical controls on the desktop controller (e.g. rotary encoders for tab switching and scrolling, push buttons for quick actions) | Free GPIOs, enclosure |
| Large desktop panel | Second, larger desktop controller on an ESP32-P4 (7" or 10.1") including the local map view; uses the same bridge and MQTT topics | Bridge, map channel |

Topic drafts for these features are in [`bridge/README.md`](bridge/README.md).

## Requirements

- Fallout 4 on PC (Steam), Pip-Boy App enabled in game settings
- MQTT broker reachable from the gaming PC and the ESP32
- ESPHome (uses the shared [`esphome_basics`](https://github.com/CzarofAK/esphome_basics) package)
