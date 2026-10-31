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
- The user confirmed in-game that adjusting the 小田急川崎線 distances improved the diagram. Diagram station positions are based on shortest-path distances through the track-circuit graph from the origin, not `DiagramViews.csv` station order or only the planned train route. When calibrating station spacing, check alternate/shortcut paths and both platform tracks as well as the planned route.
- The distance reference used for 新宿〜新百合ヶ丘 is the [2003 小田急小田原線 source](https://tanaken73.gozaru.jp/database/o-odawara.html); cumulative km are 新宿 0.0, 南新宿 0.8, 参宮橋 1.5, 代々木八幡 2.7, 代々木上原 3.5, 東北沢 4.2, 下北沢 4.9, 世田谷代田 5.6, 梅ヶ丘 6.3, 豪徳寺 7.0, 経堂 8.0, 千歳船橋 9.2, 祖師ヶ谷大蔵 10.6, 成城学園前 11.6, 喜多見 12.7, 狛江 13.8, 和泉多摩川 14.4, 登戸 15.2, 向ヶ丘遊園 15.8, 生田 17.9, 読売ランド前 19.2, 百合ヶ丘 20.5, 新百合ヶ丘 21.5. Treat these as reference values, not modern operating data.

## CSV format context

- `PlannedTrains.csv` includes fields such as `destStationId`, `direction`, `routeTrackIds`, `switchOverrides`, and `destExplicit`; `routeTrackIds` is a semicolon-separated sequence of track-circuit IDs.
- `PlannedTimings.csv` rows include train, sequence, station, track circuit, track number, arrival, departure, and pass status.
- `routes.csv` includes start/end lever IDs, track-circuit IDs, switch instructions, and conflict-route IDs.
- These examples establish file structure and specific working values, not complete format rules. Treat interpretations as provisional, check comparable maps such as Tokyo Monorail Workshop map `3812026627`, and verify behavior in game.
