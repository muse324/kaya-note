# SOUND_DESIGN

## 音の役割

音は演出ではなく、
「存在の立ち上がり」を表す。

通知音・効果音・BGMにはしない。

空間に何かが現れる瞬間の、
痕跡的な響きとして扱う。

---

## 現在の構造

音は intro を基本とするが、intro のみに限定しない。

現状では intro sound に加え、新規入力取得時にも playPopSound が鳴る。

後日、管理画面から sound あり / なし を選択できるようにする。
この選択肢は現在未実装。

---

## 現在の実装

### 和音

- 高音寄り
- 広い音域
- 半音衝突を避ける
- 微小時間ズレあり
- 長めの減衰
- compressor 使用

### アルペジオ

- accelerando → ritardando
- 非線形 timing curve
- gesture 的時間構造

---

## 避けること

- 派手なSE
- UIフィードバック音
- 常時BGM
- 過剰な残響
- cinematic化
- 感情誘導しすぎる音

---

## 未解決

- chord decay の質感
- arpeggio curve の自然さ
- sound あり / なし 設定
- 実空間での音量
- スピーカー環境差
