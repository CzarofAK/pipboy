# Pip-Boy Companion protocol

## Background

Bethesda released the official *Fallout Pip-Boy* companion app (iOS/Android) for
Fallout 4. It connects to the game over the local network and shows inventory, stats,
map and radio, and can trigger actions such as equipping items.

- The app has been removed from the Google Play Store due to incompatibilities with
  current store requirements. On Android it is only available as a sideloaded APK.
- Whether the PC version on the current game build (Anniversary update, 1.11.x) still
  connects reliably is **not confirmed** – reports are mixed. The connection test below
  answers this for our setup.

## Protocol (as known from community reverse engineering)

- **Discovery:** UDP broadcast; the game answers with its address.
- **Connection:** TCP stream. On connect the game sends the full Pip-Boy database
  (a tree of all Pip-Boy values), then incremental updates.
- **Additional channels:** local map images.
- **Commands (RPC):** the client can send commands back to the game (e.g. use item,
  change radio station).

## Existing libraries

| Project | Language | What it does |
| --- | --- | --- |
| [matzman666/PyPipboy](https://github.com/matzman666/PyPipboy) | Python 3 | Event-driven client: autodiscovery, connection handling, data and local map updates, sending commands. Basis for PyPipboyApp (desktop GUI) |
| [NimVek/pipboy](https://github.com/NimVek/pipboy) | Python | CLI to discover/connect, get/set values in the database, run as proxy (MitM) or as server for the app |
| [rgbkrk/pipboy](https://github.com/rgbkrk/pipboy) (pipboylib) | Node.js | Experimental desktop app |

These projects date from 2015/16 and are no longer maintained. As far as known,
Bethesda has not changed the protocol since.

## Connection test (≈10 minutes, before investing in the bridge)

1. In Fallout 4: *Settings → Gameplay → Pip-Boy App* → enabled. Restart the game and
   load a save (the character must already have the Pip-Boy).
2. On the gaming PC:
   ```
   git clone https://github.com/NimVek/pipboy
   cd pipboy
   python -m pip install .
   pipboy
   ```
3. In the pipboy shell:
   ```
   discover
   connect 127.0.0.1
   get $.PlayerInfo.PlayerName
   ```
4. **Expected:** the character name is returned → protocol works, continue with the
   bridge.
5. **If nothing comes back:** allow Fallout 4 through the Windows Firewall for private
   networks and try again.

## Result

- [ ] Test done – result: _pending_
