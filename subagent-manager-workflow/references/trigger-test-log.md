# トリガーテストログ（subagent-manager-workflow）

## テストケース記録

| date | skill | category | input | expected | actual | result | fix |
|---|---|---|---|---|---|---|---|
| 2026-02-15 | subagent-manager-workflow | positive | PMとして進行だけ担当し、実装は分担して進めたい | 発火して処理する | 発火して処理する | pass | - |
| 2026-02-15 | subagent-manager-workflow | positive | 実装、レビュー、テスト、コミットを担当分離で進めたい | 発火して処理する | 発火して処理する | pass | - |
| 2026-02-15 | subagent-manager-workflow | positive | 並列で複数機能を進め、依存だけ管理したい | 発火して処理する | 発火して処理する | pass | - |
| 2026-02-15 | subagent-manager-workflow | positive | 進捗管理と意思決定ゲートだけを中央で運用したい | 発火して処理する | 発火して処理する | pass | - |
| 2026-02-15 | subagent-manager-workflow | positive | サブエージェント成果物を統合して最終報告したい | 発火して処理する | 発火して処理する | pass | - |
| 2026-02-15 | subagent-manager-workflow | negative | アシスタント単独でコードを書いてほしい | 発火せず他skillへ委譲する | 発火せず他skillへ委譲する | pass | - |
| 2026-02-15 | subagent-manager-workflow | negative | 仕様検討なしで即時に実装とコミットを完了してほしい | 発火せず他skillへ委譲する | 発火せず他skillへ委譲する | pass | - |
| 2026-02-15 | subagent-manager-workflow | negative | サブエージェントを使わずにPMと実装を兼務してほしい | 発火せず他skillへ委譲する | 発火せず他skillへ委譲する | pass | - |
| 2026-02-15 | subagent-manager-workflow | negative | 単発の雑談だけをしたい | 発火せず他skillへ委譲する | 発火せず他skillへ委譲する | pass | - |
| 2026-02-15 | subagent-manager-workflow | negative | 調査結果だけを短く返してほしい | 発火せず他skillへ委譲する | 発火せず他skillへ委譲する | pass | - |
| 2026-02-15 | subagent-manager-workflow | ambiguous | 担当分担はしたいが、誰がどこまでやるか未定 | 発火し、短い確認質問を返して判定する | 発火し、短い確認質問を返して判定する | pass | - |
| 2026-02-15 | subagent-manager-workflow | ambiguous | 並列化したいが依存関係が不明 | 発火し、短い確認質問を返して判定する | 発火し、短い確認質問を返して判定する | pass | - |
| 2026-02-15 | subagent-manager-workflow | ambiguous | ユーザー相談の条件が決まっていない | 発火し、短い確認質問を返して判定する | 発火し、短い確認質問を返して判定する | pass | - |
| 2026-02-15 | subagent-manager-workflow | boundary | PM運用依頼と同時にアシスタント直実装依頼が来る | 発火し、PM管理範囲のみ処理して直実装依頼は委譲する | 発火し、PM管理範囲のみ処理して直実装依頼は委譲する | pass | - |
| 2026-02-15 | subagent-manager-workflow | boundary | 並列実行依頼と単一路線での厳格順次実行依頼が混在する | 発火し、依存関係を満たす範囲で並列化し、制約を明示して処理する | 発火し、依存関係を満たす範囲で並列化し、制約を明示して処理する | pass | - |
| 2026-02-15 | subagent-manager-workflow | boundary | 技術判断とプロダクト判断が混在する相談が来る | 発火し、プロダクト判断のみユーザー相談し、技術判断は委譲運用で処理する | 発火し、プロダクト判断のみユーザー相談し、技術判断は委譲運用で処理する | pass | - |

## quality gate 判定

- frontmatter: pass
- trigger precision: pass
- reproducibility: pass
- japanese quality: pass
- maintainability: pass
- validation logs: pass
- command sequence run: pass
- description diff impact: pass

## quick_validate

- command: `uv run --with pyyaml python /home/shiyui/.codex/skills/.system/skill-creator/scripts/quick_validate.py /home/shiyui/.codex/skills/subagent-manager-workflow`
- result: pass
- reason: frontmatter と構造の最小検証を完了
