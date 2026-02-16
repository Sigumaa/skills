---
name: plan-governed-subagent-workflow
description: このskillは、`.codex/PROJECT_PLAN.md` と `.codex/PLAN_PROGRESS.md` を正本にして作業を統制し、実装・レビュー・テスト・コミットをサブエージェントへ委譲して進行管理する。開始時に対象フェーズと対象項目を明示し、並列可能な作業は並列化する。典型要求は「計画に沿って実装を進めたい」「サブエージェント分担で回したい」「pre-commitとPLAN_PROGRESS更新まで管理したい」「必要時にCI runを監視したい」。単独実装のみの依頼、計画ファイルを使わない短時間調査、他リポジトリのCI運用には使わない。
---

# 計画統制サブエージェント運用スキル

## Overview
- `.codex/PROJECT_PLAN.md` と `.codex/PLAN_PROGRESS.md` を基準に、計画固定で進行管理する。
- アシスタント自身はPM専任で進行し、実装・レビュー・テスト・コミットはサブエージェントへ委譲する。
- 依存しない作業は並列実行し、意思決定が必要な論点のみユーザーへ相談する。
- CI運用が必要な場合は `gh-workflow` と連携し、run確認・再実行・監視を実施する。

## ワークフロー判定
- 次の依頼で発火する。
  - `.codex` 計画を守りながら機能開発を進めたい。
  - 複数サブエージェントへ実装、レビュー、テスト、コミットを分担したい。
  - `pre-commit`、`.codex/PLAN_PROGRESS.md` 更新、必要時のCI監視まで一体で管理したい。
- 次の依頼では発火しない。
  - 単独実装のみを求める依頼。
  - 計画ファイルを使わない単発調査や雑談。
  - `Sigumaa/calt` 以外を対象にした GitHub Actions 運用。
- 次の依頼では発火し、確認質問を返して判定する。
  - 対象フェーズ、対象項目、成果物範囲が未指定。
  - サブエージェント利用可否が不明。

## 実行手順
1. 開始前に `.codex/PROJECT_PLAN.md` と `.codex/PLAN_PROGRESS.md` を読み、現行計画と進捗の整合を確認する。
2. 着手時に `対象フェーズ` と `対象項目` を明示し、作業対象と非対象を固定する。
3. 実行計画を分解し、実装・レビュー・テスト・コミットを担当別サブエージェントへ委譲する。
4. 依存関係を判定し、独立タスクは並列化する。依存タスクのみ直列で管理する。
5. 仕様選定や優先度変更などの意思決定論点だけをユーザーへ相談し、決定後に実行を再開する。
6. 実装完了後に `.codex/PLAN_PROGRESS.md` の `実施ログ` と `次アクション` を更新する。
7. コミット前に `pre-commit run --all-files` を必須実行する。
8. CI run の監視や再実行が必要になった場合は `gh-workflow` を呼び、`gh run list --limit 1` と `gh run watch RUN_ID --exit-status` を含めて運用する。

## 禁止事項
- `.codex/PROJECT_PLAN.md` と `.codex/PLAN_PROGRESS.md` 未確認で実装を開始すること。
- 対象フェーズと対象項目を示さずに着手すること。
- 実装・レビュー・テスト・コミットをPMが単独で抱え込むこと。
- 意思決定をユーザー確認なしに確定すること。
- `pre-commit` 未実行でコミットすること。
- 実装変更を含むのに `.codex/PLAN_PROGRESS.md` を更新しないこと。
- `gh-workflow` の適用範囲外でCI運用操作を実施すること。

## 品質チェック
- 返答開始時に `対象フェーズ` と `対象項目` が明記されていること。
- サブエージェントへの委譲対象が `実装/レビュー/テスト/コミット` を含むこと。
- 並列化可能タスクと依存タスクの区別が示されていること。
- `.codex/PLAN_PROGRESS.md` の更新と `pre-commit` 実行が記録されていること。
- skill更新時は `references/trigger-test-log.md` を更新し、次で検証すること。
```bash
uv run --with pyyaml python /home/shiyui/.codex/skills/.system/skill-creator/scripts/quick_validate.py .codex/skills/plan-governed-subagent-workflow
```

## 返答方針
- 日本語で返答し、冒頭で対象フェーズと対象項目を明示する。
- 進行は「実施内容、委譲先、意思決定待ち、次アクション」を短く分けて報告する。
- ユーザー相談時は選択肢と推奨案を1つ示し、決定後は直ちに実行へ戻る。
- 失敗時は「失敗箇所、原因、復旧手順」を最小構成で提示する。
