# 品質ゲート

## 判定ルール

- 各項目を `pass` / `fail` で判定する
- `fail` が1つでもあれば修正して再検証する

## ゲート項目

1. frontmatterが適切
- `name` がkebab-case
- `description` が「何をするか」「いつ使うか」「使わない条件」を含む
- `description` が日本語200-400字を目安に収まる

2. トリガー精度
- 肯定ケース5件以上で適切に起動する
- 否定ケース5件以上で過剰適用しない
- 曖昧ケース3件以上で期待挙動を定義する
- 隣接skill境界ケース3件以上で誤発火しない

3. 手順の再現性
- 実行順が明確
- 前提条件が明確
- 成功条件が明確
- コードブロックの実行順テストが完走する

4. 日本語品質
- 用語が一貫している
- 曖昧語に依存しない
- 箇条書きと段落の責務が明確

曖昧語チェック:
- 適宜
- いい感じに
- 必要に応じて
- 適切に
- うまく
- しっかり
- きちんと
- など

5. 構造の保守性
- SKILL.mdに詰め込みすぎない
- 長文はreferencesへ分離している
- SKILL.md本文は120行以下を目安にする（超える場合は分割する）

6. 検証ログ
- `quick_validate.py` 実行結果がある
- 手動トリガーテスト結果がある
- 失敗時の修正履歴が残っている
- `description` 変更時に変更前後差分と発火範囲変化を記録する

## レビュー記録テンプレート

```text
[Skill]
- name:
- path:

[Result]
- overall: pass / fail

[Checks]
1. frontmatter: pass / fail
2. trigger precision: pass / fail
3. reproducibility: pass / fail
4. japanese quality: pass / fail
5. maintainability: pass / fail
6. validation logs: pass / fail
7. command sequence run: pass / fail
8. description diff impact: pass / fail

[Issues]
- issue:
  fix:

[Retest]
- command:
- result:
```
