# CURRENT_STATE

## 現在の実装

- intro → silence → main → guide 構造
- silence は独立modeではなく、intro text消滅後に main へ移行する余白として成立
- intro は実際の messages から1件のみ表示
- 音はintro中心だが限定しない
- 新規入力取得時にも playPopSound が鳴る
- sound あり / なし の管理画面設定は未実装
- ガイドは3テキスト後に遅延表示
- Google Spreadsheet ベース構成を正式採用
- messages / places の2シート構成
- place ごとの表示フィルタ実装済み
- input.html / view.html / setting.html が place 情報を共有
- setting.html の「この場所を使う」で選択した activePlaceId を localStorage に保存
- input.html は URL クエリ `place` から activePlaceId を取得し、再読込時にも localStorage に保存して最新の場所を維持するようになった
- view.html は QR を `input.html?place=<id>` で生成し、スマホ端末でも場所情報が受け継がれるようになった
- input.html / view.html に storage イベントを追加し、別タブで場所変更があれば即時反映
- view.html は場所変更時にテキスト表示をリセットして再読み込み
- page title は places.title を参照
- activePlaceId は localStorage に保持
- 表示フォントは Noto Sans JP

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
- intro text は activePlaceId に一致する実メッセージから1件のみ生成
- activePlaceId に一致する messages が0件の場合は place title を fallback 表示
- intro text の連続重複を避けるため recentIntroTexts を追加
- intro / emergence の過剰な重なりを避けるため recentSpawnPositions を追加

## 現在の注意点

- messages.placeId と activePlaceId が一致しない場合、その場所では inputHistory が空になる
- activePlaceId に一致する messages が0件の場合、main の自動生成と記憶再出現は実質的に発生しない
- Apps Script 側は messages / places の append 処理を維持する必要がある
- Google Sheets 読み込みに失敗した場合、places は旧 localStorage を fallback として読む
- messages 読み込み失敗時の local fallback は現在ない

## 未解決

- intro位置
- chord decay
- arpeggio curve
- sound あり / なし 設定
- layer breathing 強度

## 現地テスト用機能

- FIELD_TEST_MODE 定数を view.html に追加
- true に変更すると屋外・半屋外投影テスト向けの視認性向上モードが有効化
- テキスト透明度 1.4 倍、サイズ 1.3 倍、breathing 効果を 95-105% に縮小
- ガイドテキストも 1.1-1.2 倍に拡大
- デフォルトは false（通常表示）
