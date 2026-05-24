# SOUND_DESIGN

## 音の役割

音は演出ではなく、
「存在の立ち上がり」を表す。

通知音・効果音・BGMにはしない。

空間に何かが現れる瞬間の、
痕跡的な響きとして扱う。

---

## 現在の構造

音は intro 時のみ鳴る。

main モードでは音を鳴らさない。

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
- 実空間での音量
- スピーカー環境差