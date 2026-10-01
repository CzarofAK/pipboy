# Bridge (PyPipboy → MQTT)

**Status:** not written yet. Starts after the connection test in
[`docs/protocol.md`](../docs/protocol.md) succeeds.

## Planned design

- Runs on the gaming PC next to Fallout 4.
- Connects to the game via [PyPipboy](https://github.com/matzman666/PyPipboy).
- Publishes only the values the display needs, retained, under `pipboy/…`.
- Subscribes to `pipboy/cmd/…` and forwards commands to the game.

## Draft MQTT topics

| Topic | Direction | Content |
| --- | --- | --- |
| `pipboy/status` | bridge → | `online` / `offline` (LWT) |
| `pipboy/player/name` | bridge → | Character name |
| `pipboy/player/level` | bridge → | Level |
| `pipboy/player/hp` | bridge → | Current / max HP |
| `pipboy/player/ap` | bridge → | Current / max AP |
| `pipboy/player/rad` | bridge → | Radiation |
| `pipboy/player/weight` | bridge → | Current / max carry weight |
| `pipboy/quest/active` | bridge → | Active quest name |
| `pipboy/world/time` | bridge → | In-game time |
| `pipboy/radio/station` | bridge → | Current radio station |
| `pipboy/cmd/use_stimpak` | → bridge | Use a Stimpak |
| `pipboy/cmd/use_radaway` | → bridge | Use RadAway |
| `pipboy/cmd/radio_off` | → bridge | Turn radio off |

Topic names are a draft and will be finalised together with the bridge.
