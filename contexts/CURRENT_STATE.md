# CURRENT_STATE

## 現在の実装

- intro → silence → main → guide 構造
- 音はintroのみ
- ガイドは3テキスト後に遅延表示
- Google Spreadsheet ベース構成へ移行中
- messages / places の2シート構成
- place ごとの表示フィルタ実装済み
- input.html / view.html / setting.html が place 情報を共有
- page title は places.title を参照
- activePlaceId は localStorage に保持

## 現在のスプレッドシート構造

### messages

columns:

- timestamp
- text
- weight
- placeId
- placeName
- date
- lat
- lng

### places

columns:

- id
- name
- title
- date
- locationLabel

## 現在の状態

- places sheet の読み込み成功
- setting.html から place 追加成功
- input.html の title 切替成功
- view.html の title 切替成功
- view.html は messages を activePlaceId でフィルタ
- view.html の Spreadsheet ID は正しい ID に修正済み
- intro text が Google Sheets 非同期ロード後に生成される構造へ変更済み
- intro text の連続重複を避けるため recentIntroTexts を追加
- intro / emergence の過剰な重なりを避けるため recentSpawnPositions を追加

## 現在の注意点

- messages.placeId と activePlaceId が一致しない場合、その場所では inputHistory が空になる
- 確認時点で fukuchisha の messages は0件
- Apps Script 側は messages / places の append 処理を維持する必要がある
- Google Sheets 読み込みに失敗した場合、places は旧 localStorage を fallback として読む

## 未解決

- intro位置
- chord decay
- arpeggio curve
- layer breathing 強度
- 実展示環境での visibility 調整
