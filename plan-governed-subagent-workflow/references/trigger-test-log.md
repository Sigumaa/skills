# トリガーテストログ（plan-governed-subagent-workflow）

## テストケース記録

| date | skill | category | input | expected | actual | result | fix |
|---|---|---|---|---|---|---|---|
| 2026-02-15 | plan-governed-subagent-workflow | positive | `.codex` 計画を前提に、サブエージェントへ実装とレビューを分担したい | 発火して処理する | 発火して処理する | pass | - |
| 2026-02-15 | plan-governed-subagent-workflow | positive | 対象フェーズを固定して、テストとコミットを委譲管理したい | 発火して処理する | 発火して処理する | pass | - |
| 2026-02-15 | plan-governed-subagent-workflow | positive | `PLAN_PROGRESS` 更新と `pre-commit` 実行まで含めて進行してほしい | 発火して処理する | 発火して処理する | pass | - |
| 2026-02-15 | plan-governed-subagent-workflow | positive | 並列可能タスクを分けて同時進行したい | 発火して処理する | 発火して処理する | pass | - |
| 2026-02-15 | plan-governed-subagent-workflow | positive | push後のCI監視まで含めて運用したい | 発火して処理する | 発火して処理する | pass | `gh-workflow` 連携手順を明記 |
| 2026-02-15 | plan-governed-subagent-workflow | negative | 単独で実装だけしてほしい | 発火せず他手順で処理する | 発火せず他手順で処理する | pass | - |
| 2026-02-15 | plan-governed-subagent-workflow | negative | `.codex` 計画なしで単発の調査回答だけほしい | 発火せず他手順で処理する | 発火せず他手順で処理する | pass | - |
| 2026-02-15 | plan-governed-subagent-workflow | negative | `Sigumaa/calt` 以外のリポジトリで `gh run` を操作したい | 発火せず他skillへ委譲する | 発火せず他skillへ委譲する | pass | - |
| 2026-02-15 | plan-governed-subagent-workflow | negative | `.github/workflows` の実装変更だけしたい | 発火せず他手順で処理する | 発火せず他手順で処理する | pass | - |
| 2026-02-15 | plan-governed-subagent-workflow | negative | 雑談として開発体制の感想だけ聞きたい | 発火せず他手順で処理する | 発火せず他手順で処理する | pass | - |
| 2026-02-15 | plan-governed-subagent-workflow | ambiguous | 対象フェーズ未指定で「計画に沿って進めて」と依頼 | 発火し、確認質問を返して判定する | 発火し、確認質問を返して判定する | pass | - |
| 2026-02-15 | plan-governed-subagent-workflow | ambiguous | サブエージェント利用可否が不明なまま委譲運用を依頼 | 発火し、確認質問を返して判定する | 発火し、確認質問を返して判定する | pass | - |
| 2026-02-15 | plan-governed-subagent-workflow | ambiguous | CI監視希望だが `gh` 認証状態が不明 | 発火し、確認質問を返して判定する | 発火し、確認質問を返して判定する | pass | - |
| 2026-02-15 | plan-governed-subagent-workflow | boundary | 計画統制委譲運用と、実装をPM単独で即実施する要求が同時に来る | 発火し、委譲原則を維持して単独実装要求を切り分ける | 発火し、委譲原則を維持して単独実装要求を切り分ける | pass | - |
| 2026-02-15 | plan-governed-subagent-workflow | boundary | `.codex` 計画維持と `Sigumaa/calt` 以外のCI監視を同時依頼 | 発火し、CI監視は対象repo外として切り分ける | 発火し、CI監視は対象repo外として切り分ける | pass | - |
| 2026-02-15 | plan-governed-subagent-workflow | boundary | 委譲運用の途中で優先度変更判断が必要になる | 発火し、意思決定のみユーザー相談して再開する | 発火し、意思決定のみユーザー相談して再開する | pass | - |

## quality gate 判定

- frontmatter: pass
- trigger precision: pass
- delegation coverage: pass
- plan sync: pass
- ci linkage: pass
- japanese quality: pass
- maintainability: pass

## quick_validate

- command: `uv run --with pyyaml python /home/shiyui/.codex/skills/.system/skill-creator/scripts/quick_validate.py .codex/skills/plan-governed-subagent-workflow`
- result: pass
- reason: frontmatter、必須ファイル構成、agent metadata の検証を通過
