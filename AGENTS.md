# AGENTS.md

Before making changes, always read:

- context/PROJECT_RULES.md
- context/CURRENT_STATE.md
- context/FORBIDDEN_CHANGES.md

If relevant, also read:

- context/SOUND_DESIGN.md
- context/VISUAL_DESIGN.md
- context/EXHIBITION_CONTEXT.md

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
