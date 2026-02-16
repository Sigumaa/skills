# Proposed Plan 正本契約

## 目的
- `.codex/PROPOSED_PLAN.md` を、Plan mode確定後の唯一の実装正本として定義する。
- 暗黙知を省略せず、委譲可能な粒度まで明示する。

## 出力ルール
- 出力先は必ず `.codex/PROPOSED_PLAN.md` とする。
- 見出し順序は本ドキュメントの `PP-01` から `PP-10` を固定する。
- 各セクションに `参照:` 行を1つ以上記載し、根拠ファイルを示す。

## 必須セクション

| section_id | 見出し | 最小記載基準 |
|---|---|---|
| PP-01 | Plan Commitment Summary | 目的、期限、完了条件をそれぞれ1行以上 |
| PP-02 | Current Plan Context | `PROJECT_PLAN` と `PLAN_PROGRESS` の対象フェーズ、差分有無、整合判定 |
| PP-03 | Scope and Success Criteria | 対象スコープ、非対象スコープ、受け入れ基準を各1項目以上 |
| PP-04 | Dependencies and Constraints | 依存関係、環境制約、外部要因を各1項目以上 |
| PP-05 | Component Breakdown | 各機能部品に `名前` `目的` `依存` `担当` を記載 |
| PP-06 | Subagent Assignment | 各担当に `依頼タイミング` `完了条件` `返却物` を記載 |
| PP-07 | Parallelism and Sequencing | 並列可否、直列化理由、待ち合わせ条件を記載 |
| PP-08 | Quality Gates and Tests | 必須テスト、品質ゲート、失敗時の戻し先を記載 |
| PP-09 | Risks and Unknowns | リスク、未確定事項、相談が必要な gate_id を記載 |
| PP-10 | Communication and Reporting | 中間報告頻度、最終報告形式、エスカレーション条件を記載 |

## 記載基準
- 各セクションは2文以上記載する。
- `PP-05` と `PP-06` は、対象機能部品数と同数の行を持つ。
- `PP-09` は `DG-xx` 形式のゲートIDを1件以上記載する。

## 禁止事項
- 1行要約だけでセクションを終了すること。
- `適宜` `必要に応じて` `詳細は実装時に判断` などの曖昧語で判断を先送りすること。
- `TODO` `TBD` `未確定` を残したまま委譲へ進むこと。
- `.codex/PROPOSED_PLAN.md` と異なる前提で委譲文を作成すること。
