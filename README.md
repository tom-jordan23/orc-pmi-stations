# ORC PMI Station Control

Remote station mode control for PMI (Palang Merah Indonesia) ORC river monitoring stations.

## How it works

Each station checks its `station_mode` file on every boot. If the file contains `maintenance`, the station stops its capture daemon and stays awake for remote access. If it contains `production` (or the file is unreachable), the station operates normally.

## Stations

| Station | Mode file | Power |
|---------|-----------|-------|
| Sukabumi | `pi/sukabumi/station_mode` | Solar (duty-cycles 10min ON / 5min OFF) |
| Jakarta | `pi/jakarta/station_mode` | AC (always on) |

## Switching to maintenance mode

1. Edit the station's `station_mode` file on GitHub (click the pencil icon)
2. Change `production` to `maintenance`
3. Commit the change
4. Wait for the station's next boot cycle (up to 15 minutes for Sukabumi)
5. The station will stay awake and accessible via Pangolin/SSH

## Switching back to production

1. Edit the `station_mode` file
2. Change `maintenance` to `production`
3. Commit the change
4. Reboot the station (or wait for the next power cycle)

## Safety

- If GitHub is unreachable, stations default to **production** mode (fail-safe)
- Maintenance mode does NOT change the Witty Pi power schedule — Sukabumi still power-cycles (10 ON / 5 OFF) but stays awake for the full ON window instead of shutting down after ~3 minutes
- Jakarta stays on indefinitely in maintenance mode
