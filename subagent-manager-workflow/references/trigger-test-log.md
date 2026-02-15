# トリガーテストログ（subagent-manager-workflow）

## テストケース記録

| date | skill | category | input | expected | actual | result | fix |
|---|---|---|---|---|---|---|---|
| 2026-02-15 | subagent-manager-workflow | positive | PMとして進行だけ担当し、実装は分担して進めたい | 発火して処理する | 発火して処理する | pass | - |
| 2026-02-15 | subagent-manager-workflow | positive | Plan確定後に `.codex` と `.github` を整備してから着手したい | 発火して処理する | 発火して処理する | pass | - |
| 2026-02-15 | subagent-manager-workflow | positive | 実装、レビュー、テスト、コミットを担当分離で進めたい | 発火して処理する | 発火して処理する | pass | - |
| 2026-02-15 | subagent-manager-workflow | positive | 並列で複数機能を進め、依存だけ管理したい | 発火して処理する | 発火して処理する | pass | - |
| 2026-02-15 | subagent-manager-workflow | positive | push後CIを監視しつつ進行管理したい | 発火して処理する | 発火して処理する | pass | - |
| 2026-02-15 | subagent-manager-workflow | positive | 並列可否を判定表で機械的に決めたい | 発火し `orchestration-rules.md` を適用する | 発火し `orchestration-rules.md` を適用する | pass | - |
| 2026-02-15 | subagent-manager-workflow | positive | 実装/レビュー/テスト/コミットごとに固定委譲文を使いたい | 発火し `delegation-prompt-templates.md` を適用する | 発火し `delegation-prompt-templates.md` を適用する | pass | - |
| 2026-02-15 | subagent-manager-workflow | positive | テスト失敗とCI失敗で復旧手順を分けて運用したい | 発火し `failure-recovery-playbook.md` を適用する | 発火し `failure-recovery-playbook.md` を適用する | pass | - |
| 2026-02-15 | subagent-manager-workflow | positive | 進捗報告と完了報告を固定項目で統一したい | 発火し `report-format.md` を適用する | 発火し `report-format.md` を適用する | pass | - |
| 2026-02-15 | subagent-manager-workflow | negative | アシスタント単独でコードを書いてほしい | 発火せず他skillへ委譲する | 発火せず他skillへ委譲する | pass | - |
| 2026-02-15 | subagent-manager-workflow | negative | サブエージェントを使わずにPMと実装を兼務してほしい | 発火せず他skillへ委譲する | 発火せず他skillへ委譲する | pass | - |
| 2026-02-15 | subagent-manager-workflow | negative | 単発の雑談だけをしたい | 発火せず他skillへ委譲する | 発火せず他skillへ委譲する | pass | - |
| 2026-02-15 | subagent-manager-workflow | negative | 調査結果だけを短く返してほしい | 発火せず他skillへ委譲する | 発火せず他skillへ委譲する | pass | - |
| 2026-02-15 | subagent-manager-workflow | negative | `.github/workflows` の設計だけ単独で依頼したい | 発火せず他skillへ委譲する | 発火せず他skillへ委譲する | pass | - |
| 2026-02-15 | subagent-manager-workflow | negative | PMが直接実装してそのままコミットしてほしい | 発火せず他skillへ委譲する | 発火せず他skillへ委譲する | pass | - |
| 2026-02-15 | subagent-manager-workflow | ambiguous | ブートストラップ対象ファイルの責務が未定義 | 発火し、短い確認質問を返して判定する | 発火し、短い確認質問を返して判定する | pass | - |
| 2026-02-15 | subagent-manager-workflow | ambiguous | 並列化したいが依存関係が不明 | 発火し、短い確認質問を返して判定する | 発火し、短い確認質問を返して判定する | pass | - |
| 2026-02-15 | subagent-manager-workflow | ambiguous | CI品質ゲートの強制度合いが未定義 | 発火し、短い確認質問を返して判定する | 発火し、短い確認質問を返して判定する | pass | - |
| 2026-02-15 | subagent-manager-workflow | ambiguous | `.github/workflows` はあるが品質ゲートとして十分か不明 | 発火し、`decision-gates.md` で確認質問を返して判定する | 発火し、`decision-gates.md` で確認質問を返して判定する | pass | - |
| 2026-02-15 | subagent-manager-workflow | boundary | PM運用依頼と同時にアシスタント直実装依頼が来る | 発火し、PM管理範囲のみ処理して直実装依頼は委譲する | 発火し、PM管理範囲のみ処理して直実装依頼は委譲する | pass | - |
| 2026-02-15 | subagent-manager-workflow | boundary | `.codex` は存在するが `.github/workflows` がない | 発火し、不足分のみブートストラップして処理する | 発火し、不足分のみブートストラップして処理する | pass | - |
| 2026-02-15 | subagent-manager-workflow | boundary | 技術判断とプロダクト判断が混在する相談が来る | 発火し、プロダクト判断のみユーザー相談する | 発火し、プロダクト判断のみユーザー相談する | pass | - |
| 2026-02-15 | subagent-manager-workflow | boundary | `.codex` は揃っているが必須項目が欠落している | 発火し、欠落責務だけ最小差分で補完する | 発火し、欠落責務だけ最小差分で補完する | pass | - |
| 2026-02-15 | subagent-manager-workflow | boundary | 復旧を2サイクル実施しても品質ゲートが通らない | 発火し、`decision-gates.md` に従いユーザー相談へ遷移する | 発火し、`decision-gates.md` に従いユーザー相談へ遷移する | pass | - |

## quality gate 判定

- frontmatter: pass
- trigger precision: pass
- reproducibility: pass
- japanese quality: pass
- maintainability: pass
- validation logs: pass
- command sequence run: pass
- orchestration rules linkage: pass
- delegation template coverage: pass
- failure recovery coverage: pass
- decision gate clarity: pass
- report format consistency: pass
- description diff impact: pass
  - 変更点: descriptionを200-400字目安へ再定義し、利用条件と非適用条件、再現用参照資料を明示

## quick_validate

- command: `uv run --with pyyaml python /home/shiyui/.codex/skills/.system/skill-creator/scripts/quick_validate.py /home/shiyui/.codex/skills/subagent-manager-workflow`
- result: pass
- reason: frontmatter と構造の最小検証を完了
