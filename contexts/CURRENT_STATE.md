# CURRENT_STATE

## 現在の実装

- intro → main → guide 構造
- 音はintroのみ
- ガイドは3テキスト後に遅延表示

## 未解決

- intro位置
- chord decay
- arpeggio curve

# CURRENT_STATE

## 現在の実装

- intro → silence → main → guide 構造
- 音はintroのみ
- ガイドは3テキスト後に遅延表示
- Google Spreadsheet ベース構成へ移行中
- messages / places の2シート構成
- place ごとの表示フィルタ実装中
- input.html / view.html / settings.html が place 情報を共有
- page title は places.title を参照

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
- settings.html から place 追加成功
- input.html の title 切替成功
- activePlaceId は localStorage に保持
- intro text が Google Sheets 非同期ロード後に生成される構造へ変更済み

## 現在の問題

- intro text がまだ表示されないケースがある
- place filter と intro 初期化タイミングの競合可能性
- loadTextsFromGoogleSheet() 後の texts.push が正常動作しているか未確認
- Console logging による原因調査が必要

## 未解決

- intro位置
- chord decay
- arpeggio curve
- layer breathing 強度
- 実展示環境での visibility 調整