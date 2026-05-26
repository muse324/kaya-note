# title

かやのおと Google Spreadsheet移行・place管理・intro安定化

# date

2026-05-24 15:42

# tags

* handover
* chatgpt
* codex
* project/kaya-note
* p5js
* installation
* spreadsheet
* exhibition

# purpose

* 「かやのおと」展示システムを、Google Spreadsheet ベースの place 管理構造へ移行する
* 通行型インスタレーションとして、場所ごとの言葉・記憶・タイトルを管理可能にする
* localStorage依存を減らし、複数PC・複数展示環境で共有可能にする
* intro → silence → emergence の時間構造を維持したまま、place filter と共存させる
* 展示運用に耐える低保守・ローカル復旧可能な構造を維持する

# current_state

## 現在できていること

* Google Spreadsheet ベース構成へ移行中
* places sheet 読み込み成功
* settings.html から place 追加成功
* input.html の title 切替成功
* activePlaceId は localStorage に保持
* page title は places.title を参照
* input / view / settings が place 情報を共有
* messages / places の2シート構成
* Apps Script appendRow 動作成功

## 実装済み内容

### place構造

place は以下を持つ：

* id
* name
* title
* date
* locationLabel

### messages構造

messages は以下を持つ：

* timestamp
* text
* weight
* placeId
* placeName
* date
* lat
* lng

### Apps Script

doPost(e) に：

* addPlace
* addMessage

分岐追加済み。

append-only構造。

### view.html

* active place 読み込み
* place filter
* title切替
* intro text 非同期ロード対応

### input.html

* places.title をページタイトルへ反映
* active place fallback 対応

### settings.html

* place一覧表示
* place追加
* active place切替
* localStorage保存

## 関係ファイル

* view.html
* input.html
* settings.html
* Apps Script doPost()
* contexts/CURRENT_STATE.md
* contexts/PROJECT_RULES.md
* contexts/VISUAL_DESIGN.md
* AGENTS.md

## UI状態

* GUI最小構成
* settings.html のみ管理UI
* view/input は展示UIとして保持
* intro → silence → emergence 構造維持

## DB状態

Google Spreadsheet：

### messages sheet

columns:

* timestamp
* text
* weight
* placeId
* placeName
* date
* lat
* lng

### places sheet

columns:

* id
* name
* title
* date
* locationLabel

## API状態

Apps Script Web App：

* doPost(e)
* addPlace
* addMessage

動作確認済み。

Spreadsheet URL:
https://docs.google.com/spreadsheets/d/1l2Ebe6o6l3irnh01hgDWIVw3pPY9cH71jOD7nArO-oE/edit?usp=sharing

## 動作確認状況

確認済み：

* places sheet 読み込み
* place追加
* title切替
* activePlace 保存

未安定：

* intro text 初期生成
* intro text 重複
* 縦書き重なり

# decisions

## 決定済み方針

* Google Spreadsheet を中心DBとして使用
* append-oriented構造を維持
* 過去を書き換えない
* UIを増やさない
* TTS禁止
* fullscreen強制禁止
* Web Audio APIのみ
* p5.js単体維持
* localhost前提
* 低依存・低保守

## 表現方針

* intro は raw text
* 音は intro のみ
* 記憶は「痕跡の再出現」
* guide は UIではなく空間の一部
* ambiguity を維持
* explanation を増やしすぎない

## 採用した設計

### place管理

localStorage →
Google Spreadsheet へ移行。

ただし：

activePlaceId のみ localStorage保持。

### Apps Script

action-based：

* addPlace
* addMessage

分岐構造。

### intro

Google Sheets 非同期ロード後に intro text を生成。

## 却下した案

* framework導入
* Firebase
* React化
* collision physics
* rigid layout
* deterministic cycling
* GUI追加

# unresolved

## intro

* intro text が表示されないケースあり
* 非同期ロードタイミング問題の可能性
* place filter により inputHistory が空になる可能性
* mode === "intro" 条件未確認

## テキスト配置

* 縦書き重なりすぎ問題
* 大サイズテキスト重複
* organicさを維持したまま重なりを減らしたい

## intro重複

* 表示候補が少ないと同じ文が連続する
* recent queue導入予定

## 音

* chord decay 質感
* arpeggio curve 微調整

## 展示

* 実投影サイズ
* ネット透過率
* 黒布構造
* 通行速度との適合
* 虫環境

# next_actions

## 優先順

### 1. intro debug

Codexへ依頼：

* setup()
* loadPlacesFromGoogleSheet()
* loadTextsFromGoogleSheet()
* texts.push()

の実行順確認。

特に：

* inputHistory populated?
* place filter empty?
* mode === "intro"?
* FloatingText created?

を確認。

### 2. intro重複回避

recentIntroTexts queue 導入。

要求：

* deterministicにしない
* recentのみ避ける
* organic維持

### 3. spawn位置改善

recent spawn positions を保持。

* severe overlap回避
* slight overlap許容
* grid禁止
* collision engine禁止

### 4. 実展示確認

* 投影距離
* 文字サイズ
* 黒布
* 蚊帳透過
* brightness

## ChatGPTに次聞く候補

* organic layout 改善案
* intro timing refinement
* Web Audio decay shaping
* memory layer breathing design
* exhibition spatial tuning

# related_files

* path:
  /Users/hashida/Documents/vsc-workspace/kaya-note/

* file:
  view.html

* file:
  input.html

* file:
  settings.html

* file:
  AGENTS.md

* file:
  contexts/CURRENT_STATE.md

* file:
  contexts/PROJECT_RULES.md

* file:
  contexts/FORBIDDEN_CHANGES.md

* file:
  contexts/VISUAL_DESIGN.md

* file:
  contexts/SOUND_DESIGN.md

* migration:
  localStorage → Google Spreadsheet

* route:
  Apps Script Web App doPost()

* model:
  place-based memory filtering

# related_urls

* source_url:
  https://docs.google.com/spreadsheets/d/1l2Ebe6o6l3irnh01hgDWIVw3pPY9cH71jOD7nArO-oE/edit?usp=sharing

* localhost:
  http://localhost:8000/view.html

* localhost:
  http://localhost:8000/input.html

* localhost:
  http://localhost:8000/settings.html

# notes

* CURRENT_STATE.md が重複している（旧版＋新版が両方残っている）
* contexts/ と context/ が混在している可能性あり
* Apps Script変更時は必ず再デプロイ必要
* CSV URL直接確認で debug 可能
* Spreadsheet共有設定は「リンクを知っている全員・閲覧者」
* intro問題は architecture rewrite ではなく async timing 問題の可能性が高い
* 表示重なりは「整理されたUI」にしないこと
* 「美しく不均衡」な状態を維持する
* history-0407v1 / history-0407v2 の思想を継承中

# restart_prompt

以下は次チャット冒頭に貼る用：

```text
Read:
- AGENTS.md
- contexts/CURRENT_STATE.md
- contexts/PROJECT_RULES.md
- contexts/FORBIDDEN_CHANGES.md
- contexts/VISUAL_DESIGN.md

We are continuing development of the “かやのおと” installation system.

Current state:
- Google Spreadsheet based place system implemented
- messages / places two-sheet structure
- Apps Script addPlace/addMessage working
- title switching works
- place filtering implemented
- intro async initialization partially unstable

IMPORTANT:
Do NOT rewrite architecture.
Do NOT refactor unrelated code.
Preserve:
- intro → silence → emergence
- poetic ambiguity
- low dependency
- p5.js standalone structure
- exhibition-oriented behavior

Current priorities:
1. stabilize intro text appearance
2. reduce repeated intro texts
3. reduce excessive vertical text overlap
4. preserve organic composition

Focus on minimal surgical fixes only.
```
