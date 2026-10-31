# CustomMaps 作業ルール

## データの扱い

- このリポジトリのファイルはゲームデータです。
- CSVを編集するときは、文字コード、BOM、改行コード、列の順序、末尾の空列、値の書式をそのまま保ちます。
- ユーザーが動作を確認したら、gitコミットを作ります。mdやゲーム側による整形も一緒に含めます。
- 動作確認できた新たな知見は、積極的にmdに反映してください。

## リポジトリとマップ

- `steam_autocloud.vdf` は Steam が自動生成するファイルで、Git の対象外です。
- 比較用マップ: 東京モノレールのワークショップマップ(ID `3812026627`)は、リポジトリの外の `C:\Program Files (x86)\Steam\steamapps\workshop\content\4932180\3812026627` にあります。データは `Data` の中です。
- 小田急川崎線のマップは `map_20261025170633_b3fd` です。
  - データ: `map_20261025170633_b3fd\Data\map_20261025170633_b3fd`
  - 作業中の時刻表: 上記の `Scenarios\MyDiagram`

## 小田急川崎線の現状(ゲーム内で確認済み)

- 列車は 表参道 → 代々木上原(停車) → 新百合ヶ丘 の順に走ります。時刻表の時刻は推定値で、実際の所要時間ではありません。
- 方向が `-1` の列車は、双方向の `TC_0058` を通る経路です。
- 駅間距離を調整したところ、ダイヤグラムが改善しました。
- ダイヤグラム上の駅の位置は、起点から軌道回路グラフをたどった最短経路の距離で決まります。`DiagramViews.csv` の駅順や、予定列車の経路だけでは決まりません。駅間隔を調整するときは、別経路や近道、両方のホーム線も確認します。

## CSVの形式メモ

- `PlannedTrains.csv`: `destStationId`、`direction`、`routeTrackIds`、`switchOverrides`、`destExplicit` などの列があります。`routeTrackIds` は軌道回路IDをセミコロンでつないだものです。
- `PlannedTimings.csv`: 列車、順序、駅、軌道回路、線路番号、到着、出発、通過かどうか、の行です。
- `routes.csv`: 始点と終点のレバーID、軌道回路ID、分岐器の指定、競合する進路のIDなどがあります。
-  ホーム長のチェックで見られているのは、駅のホームの軌道回路について `track_circuits.csv` の `length` です。`coordinates.csv` のポリゴンの大きさではありません。

## 外部資料

- 駅間距離：[2003年の小田急小田原線の資料](https://tanaken73.gozaru.jp/database/o-odawara.html)
- 軌道回路(閉塞)：[BVE小田急線](~/Downloads/odakyuline_yuen_dds)
