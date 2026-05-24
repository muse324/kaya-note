# history-0524

2026-05-24 の実装記録。

## 目的

「かやのおと」の場所管理を、localStorage 中心の構成から Google Spreadsheet ベースの構成へ移行した。

ただし、作品の表示・音・時間構造は変更せず、既存の p5.js 単体構成、低依存、localhost 運用、展示現場での復旧しやすさを維持する方針で進めた。

## Spreadsheet 構成

messages シート:

- timestamp
- text
- weight
- placeId
- placeName
- date
- lat
- lng

places シート:

- id
- name
- title
- date
- locationLabel

## view.html

Google Spreadsheet から places / messages の2シートを CSV として読む構成に変更した。

places シートから active place を解決し、`place.title` を `document.title` に反映するようにした。

active place は `localStorage` の `kaya-note-active-place-id` を参照する。場所一覧自体は Spreadsheet を正とし、旧 localStorage の `kaya-note-places` は Sheet が読めない場合のフォールバックとして残した。

messages シートの読み込みでは、`placeId` 列が存在する場合に `CONFIG.place.activePlaceId` と一致する行だけを `inputHistory` に入れるようにした。既存CSV互換のため、`placeId` 列がないCSVでは従来通り表示できるようにした。

一度、`view.html` の `SPREADSHEET_ID` に Apps Script deployment ID が入っていたため、正しい Spreadsheet ID:

`1l2Ebe6o6l3irnh01hgDWIVw3pPY9cH71jOD7nArO-oE`

へ修正した。

## setting.html

既存ファイル名に合わせて、`settings.html` ではなく `setting.html` を管理画面として更新した。

places シートを CSV で読み込み、登録済みの場所一覧を表示するようにした。

選択中の active place ID だけを localStorage に保存する構成に変更した。

新しい場所の追加では、以下の値を Apps Script に POST する:

- action: addPlace
- sheet: places
- id
- name
- title
- date
- locationLabel

この POST は Apps Script 側で places シートへの append として処理される前提。

破壊的な上書きではなく、append-oriented な運用を前提にした。

## input.html

places シートを読み込み、active place の `title` を `document.title` と画面上の `h2` に反映するようにした。

active place がまだ localStorage にない場合は、places シートの先頭行を使い、その id を active place として保存する fallback を入れた。

送信処理、位置情報取得、Apps Script への message POST は変更していない。

## intro 周辺の調整

Google Sheets 移行後、intro text は非同期ロード後に生成される構造になった。

候補テキストが少ない場合、同じ message が繰り返し出やすかったため、`recentIntroTexts` の短い履歴を追加した。

intro 用の選択は `pickIntroLog()` に集約し、直前の text と最近使った text を可能な範囲で避けるようにした。ただし候補が少ない場合は fallback し、決定的なローテーションにはしていない。

縦書きテキストが過剰に重なる問題に対して、`recentSpawnPositions` と `pickSoftSpawnPosition()` を追加した。

直近の出現位置から近すぎる場合だけ数回再抽選する。完全な collision engine や grid layout ではなく、重なりを少し許す確率的な配置のままにした。

`FloatingText` の描画・寿命・色・速度・音の構造は変更していない。

## デバッグで確認したこと

確認時点で places シートには次の id があった:

- jrvierra
- fukuchisha
- tsunagaroom

確認時点で messages シートの `placeId` は以下だった:

- jrvierra: 96件
- tsunagaroom: 6件
- fukuchisha: 0件

そのため、active place が `fukuchisha` の場合は place filter により `inputHistory` が空になり、intro text が出ない状態になる。これはコードだけでなく Sheet 側データにも依存する。

## 現在の注意点

active place と messages.placeId が一致しない場合、その場所では表示対象が空になる。

Apps Script 側は、messages への投稿と places への追加を append として処理する必要がある。

intro の非同期ロード順は次の前提:

setup()
→ loadPlacesFromGoogleSheet()
→ applyPlaceSettings()
→ loadTextsFromGoogleSheet()
→ intro / initial text generation

今後もこの順序を崩さず、描画・音響・時間構造への大きな変更は避ける。

## 検証

各 HTML の inline script は `node --check` で構文確認した。

`view.html` については `git diff --check` でも whitespace error がないことを確認した。

