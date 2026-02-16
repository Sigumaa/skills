---
name: subagent-manager-workflow
description: 複数サブエージェント開発をPM専任で再現運用するための進行管理スキル。Plan modeで確定した計画を `.codex/PROPOSED_PLAN.md` に詳細化して書き出し、以後の実装はその正本のみを参照して進める。あわせて `.codex` と `.github` の不足を判定し、必要最小差分でブートストラップしたうえで、実装・レビュー・テスト・コミットを担当分離して委譲する。並列化判定、委譲文テンプレ、失敗復旧、相談ゲート、報告フォーマットを参照資料で固定し、別モデルでも同手順で運用できる。単独実装依頼、サブエージェント非利用、計画未確定、雑談のみでは使わない。
---

# サブエージェント進行管理ワークフロー

## Overview
- このskillは、アシスタントをPM専任に固定し、委譲オーケストレーションだけを担当する。
- Plan modeで確定した計画を `.codex/PROPOSED_PLAN.md` に展開し、以後の実装判断はこの正本だけを参照する。
- 暗黙知の省略を禁止し、実装可能な粒度まで言語化してから委譲を開始する。
- Plan確定後に `.codex` と `.github` の不足を判定し、必要最小限の補完を行う。
- 実装、レビュー、テスト、コミットは担当分離してサブエージェントへ委譲し、PMは直接実行しない。
- 並列化、失敗復旧、相談トリガー、報告様式は `references/` の固定ルールに従う。

## ワークフロー判定
- 次の依頼は発火して処理する。
  - Plan modeで確定したProposed PlanをMarkdown正本として出力したい
  - Proposed Planを唯一の情報源に固定し、実装委譲へ引き継ぎたい
  - Planを実装フェーズへ移すために運用ファイルを不足判定つきで整備したい
  - PM専任で、実装/レビュー/テスト/コミットを担当分離して委譲したい
  - 並列実行と待ち合わせ条件を固定ルールで再現したい
- 次の依頼は発火せず他skillへ委譲する。
  - アシスタント単独で実装、レビュー、テスト、コミットまで実施する依頼
  - サブエージェントを使わない運用が明示された依頼
  - Plan未確定で要件整理のみを行う依頼
  - 単発の調査や雑談のみの依頼
- 次の依頼は発火し、短い確認質問を返して判定する。
  - Proposed Planへ展開すべき前提、制約、受け入れ基準が曖昧
  - ブートストラップ対象ファイルの責務や更新許容範囲が未定義
  - 品質ゲートの強制範囲、復旧方針、相談窓口が未定義

## 実行手順
1. 依頼受領時に、成果物、期限、完了条件を3行以内で固定する。
2. Plan確定状態を確認し、`.codex/PROJECT_PLAN.md` `.codex/PLAN_PROGRESS.md` `.codex/STARTUP_CHECKLIST.md` の存在と最新性を確認する。最新性判定は、対象ファイルに現在の対象フェーズと完了条件が反映済みで矛盾がないことを基準にする。
3. ブートストラップ判定を `references/bootstrap-file-contract.md` で実施する。判定条件は次を必須化する。
   - ファイル欠落時: 対象を新規作成する。
   - ファイル存在時: 必須責務が欠落または矛盾している場合のみ更新する。
   - `.github/workflows` 判定: workflow未存在、または品質ゲート導線が未定義なら最小差分で補完する。
   - 既存運用を上書きする可能性がある場合: `references/decision-gates.md` の相談ゲートでユーザー確認する。
4. Plan modeの確定内容を `.codex/PROPOSED_PLAN.md` に書き出す。記載内容は `references/proposed-plan-contract.md` の必須セクション、最小記載基準、禁止事項に従う。
5. `.codex/PROPOSED_PLAN.md` を `references/proposed-plan-validation.md` で検証する。失敗時は不足項目を補完し、検証passまで再生成する。
6. 対象フェーズと対象項目を固定し、`PLAN_PROGRESS` の `現在の実施対象` を更新する。`現在の実施対象` には `.codex/PROPOSED_PLAN.md` の対応セクションIDを必ず記載する。
7. 作業を機能部品へ分解し、`references/orchestration-rules.md` に従って依存グラフと並列可否を決定する。分解結果は `.codex/PROPOSED_PLAN.md` の `Component Breakdown` と一致させる。
8. 待ち合わせ条件を `references/orchestration-rules.md` の規約で設定し、直列化理由を記録する。
9. 委譲時は `references/delegation-prompt-templates.md` の固定テンプレートを使い、実装/レビュー/テスト/コミットを担当分離して割り当てる。すべての委譲文に `.codex/PROPOSED_PLAN.md` の参照セクションを明記する。
10. PMの担当を `進捗管理` `依存調整` `意思決定ゲート管理` `統合報告` に限定する。PMは実装/レビュー/テスト/コミットを直接実行しない。
11. 失敗発生時は `references/failure-recovery-playbook.md` の失敗タイプ別手順で復旧し、再委譲を行う。
12. ユーザー相談要否は `references/decision-gates.md` の yes/no 判定で機械的に決定する。`.codex/PROPOSED_PLAN.md` に未確定事項が残る場合は相談ゲートを必ず判定する。
13. 中間進捗と最終報告は `references/report-format.md` の固定項目で報告する。
14. push後CI監視が必要な場合は `$gh-workflow` を併用し、最新run監視まで完了する。

## 禁止事項
- PMが実装、レビュー、テスト、コミットを直接実行すること。
- PMが修正パッチ作成、テスト実行、コミット作成を代行すること。
- Plan未確認のまま委譲タスクを開始すること。
- `.codex/PROPOSED_PLAN.md` を作成せずに委譲を開始すること。
- 暗黙知を「適宜」「必要に応じて」等の曖昧語で省略し、実装判断を口頭補完に委ねること。
- `.codex/PROPOSED_PLAN.md` の内容と矛盾する作業指示を出すこと。
- ブートストラップ判定を省略し、`.codex` / `.github` 不足を未確認のまま着手すること。
- 並列可能な部品を根拠なく直列化すること。
- 仕様や優先度の変更をユーザー相談なしで確定すること。
- 失敗時に復旧タイプを特定せず場当たりで再実行すること。

## 品質チェック
- `.codex/PROPOSED_PLAN.md` が存在し、`references/proposed-plan-contract.md` の必須セクションを満たすこと。
- `.codex/PROPOSED_PLAN.md` が `references/proposed-plan-validation.md` の検証ルールにpassしていること。
- ブートストラップ対象の判定根拠が `references/bootstrap-file-contract.md` に沿って記録されていること。
- 並列可否、依存グラフ、待ち合わせ条件が `references/orchestration-rules.md` と一致していること。
- 委譲文が `references/delegation-prompt-templates.md` の固定項目を満たしていること。
- 失敗時の復旧ログが `references/failure-recovery-playbook.md` の分類で残っていること。
- ユーザー相談の有無が `references/decision-gates.md` の判定結果で説明できること。
- 進捗報告と完了報告が `references/report-format.md` の固定項目を満たしていること。
- 実装、レビュー、テスト、コミットがすべて委譲され、PM直接実行がないこと。
- `references/trigger-test-log.md` に肯定、否定、曖昧、境界ケースの検証結果があること。
- skill更新後は次を実行すること。
```bash
uv run --with pyyaml python /home/shiyui/.codex/skills/.system/skill-creator/scripts/quick_validate.py /home/shiyui/.codex/skills/subagent-manager-workflow
```

## 返答方針
- 返答は日本語で行い、Proposed Plan正本化状況、ブートストラップ状況、委譲状況、相談ゲート判定を分けて示す。
- 進捗報告と完了報告は `references/report-format.md` の固定フォーマットを使う。
- ユーザー相談時は `references/decision-gates.md` の該当ゲートIDを示し、選択肢と推奨案を1回で提示する。
