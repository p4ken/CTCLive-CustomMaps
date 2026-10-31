# CustomMaps workspace instructions

These instructions apply to all Copilot work in this repository.

## Preserve game data

- Treat files in this repository as game data. Before editing a CSV, inspect and preserve its encoding, byte-order mark, line endings, column order, trailing empty columns, and value formatting. Make targeted edits; do not normalize unrelated rows.
- Review the resulting diff for unintended formatting or game-save changes. Preserve pre-existing changes and do not stage or commit unrelated files unless requested.
- Validate the changed data with available checks. Do not claim in-game behavior was verified unless it was tested in the game.
- Do not create a git commit until the user has tested the changes in-game and confirmed that the behavior is correct.

## Repository and map context

- This repository is the Git-tracked `CustomMaps` directory under `%USERPROFILE%\AppData\LocalLow\Tadimaru\CTCLive\CustomMaps`, on branch `main`.
- Steam generates `steam_autocloud.vdf`; it is ignored by Git.
- The Tokyo Monorail Workshop map with ID `3812026627` is installed outside this repository at `C:\Program Files (x86)\Steam\steamapps\workshop\content\4932180\3812026627`; its data is under `Data`. Use it as a comparison map when useful, and verify files there before relying on its contents.
- The 小田急川崎線 map is `map_20261025170633_b3fd`. Its data is under `map_20261025170633_b3fd\Data\map_20261025170633_b3fd`; its working timetable is under `map_20261025170633_b3fd\Data\map_20261025170633_b3fd\Scenarios\MyDiagram`.
- The user confirmed in-game that the repaired train runs 表参道 -> 代々木上原 (stop) -> 新百合ヶ丘. The timetable times are estimates, not real-world timings.
- The recorded route uses `TC_0058`, which is bidirectional, for the train whose direction is `-1`. Treat these as current map facts and verify the referenced files before relying on them after further edits.

## CSV format context

- `PlannedTrains.csv` includes fields such as `destStationId`, `direction`, `routeTrackIds`, `switchOverrides`, and `destExplicit`; `routeTrackIds` is a semicolon-separated sequence of track-circuit IDs.
- `PlannedTimings.csv` rows include train, sequence, station, track circuit, track number, arrival, departure, and pass status.
- `routes.csv` includes start/end lever IDs, track-circuit IDs, switch instructions, and conflict-route IDs.
- These examples establish file structure and specific working values, not complete format rules. Treat interpretations as provisional, check comparable maps such as Tokyo Monorail Workshop map `3812026627`, and verify behavior in game.
