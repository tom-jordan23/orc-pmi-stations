# ORC PMI Station Control

Remote station mode control for PMI (Palang Merah Indonesia) ORC river monitoring stations.

## How it works

Each station checks its `station_mode` file on every boot. If the file contains `maintenance`, the station stops its capture daemon and stays awake for remote access. If it contains `production` (or the file is unreachable), the station operates normally.

## Stations

| Station | Mode file | Power |
|---------|-----------|-------|
| Sukabumi | `pi/sukabumi/station_mode` | Solar (duty-cycles 10min ON / 5min OFF) |
| Jakarta | `pi/jakarta/station_mode` | AC (always on) |

## Switching station mode (recommended)

1. Go to **Actions** tab in this repo
2. Click **Set Station Mode** in the left sidebar
3. Click **Run workflow**
4. Select the station and mode from the dropdowns
5. Click **Run workflow**
6. Wait for the station's next boot cycle (up to 15 minutes for Sukabumi)

## Switching station mode (manual)

1. Edit the station's `station_mode` file on GitHub (click the pencil icon)
2. Change `production` to `maintenance` (or vice versa)
3. Commit the change
4. Wait for the station's next boot cycle

## Safety

- If GitHub is unreachable, stations default to **production** mode (fail-safe)
- Maintenance mode does NOT change the Witty Pi power schedule — Sukabumi still power-cycles (10 ON / 5 OFF) but stays awake for the full ON window instead of shutting down after ~3 minutes
- Jakarta stays on indefinitely in maintenance mode
