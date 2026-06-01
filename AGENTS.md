# AGENTS.md

Before making changes, always read:

- contexts/CURRENT_PROJECT.md
- contexts/CURRENT_STATE.md
- contexts/PROJECT_RULES.md
- contexts/FORBIDDEN_CHANGES.md

Role of each file:

- CURRENT_PROJECT.md
    - 作品仕様書
    - 表現意図
    - 展示条件
    - デザイン原則
    - 未解決の表現課題

- CURRENT_STATE.md
    - 実装状態書
    - システム構成
    - データ構造
    - 実装済み機能
    - 技術的制約

Consistency rules:

- CURRENT_PROJECT.md を作品意図の一次情報とする
- CURRENT_STATE.md を実装状態の一次情報とする
- 両者に矛盾がある場合は勝手に解釈せず報告する
- 実装変更時は CURRENT_STATE.md の更新要否を確認する
- 表現・展示方針変更時は CURRENT_PROJECT.md の更新要否を確認する

When both files exist:

- Preserve consistency between CURRENT_PROJECT.md and CURRENT_STATE.md
- Treat CURRENT_PROJECT.md as the source of truth for artistic intent and exhibition design
- Treat CURRENT_STATE.md as the source of truth for implementation details
- If a conflict is detected, do not silently choose one; explain the discrepancy and ask for clarification

If relevant, also read:

- contexts/SOUND_DESIGN.md
- contexts/VISUAL_DESIGN.md
- contexts/EXHIBITION_CONTEXT.md

Rules:

- Preserve project philosophy
- Prefer minimal diffs
- Never refactor unrelated code
- Ask before architectural changes
- Preserve exhibition reliability
- Prefer local, low-dependency solutions

When uncertain:

- explain assumptions
- ask concise clarification questions

Never:

- introduce unnecessary frameworks
- rewrite unrelated code
- add explicit GUI unnecessarily
- replace intentional ambiguity with conventional UX

## Development Rules

## 編集記録の追加

作成したファイル、上書きしたファイル、削除したファイル、移動したファイルが生じた場合、これらの変更箇所について

- contexts/history/HISTORY_FORMAT.md

に従って変更記録をつけること。
簡潔なコミットメッセージを提案する。
日本語で記述する。
