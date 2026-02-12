# 品質ゲート

## 判定ルール

- 各項目を `pass` / `fail` で判定する
- `fail` が1つでもあれば修正して再検証する

## ゲート項目

1. frontmatterが適切
- `name` がkebab-case
- `description` が「何をするか」と「いつ使うか」を含む

2. トリガー精度
- 肯定ケースで適切に起動する
- 否定ケースで過剰適用しない

3. 手順の再現性
- 実行順が明確
- 前提条件が明確
- 成功条件が明確

4. 日本語品質
- 用語が一貫している
- 曖昧語（適宜、いい感じ、必要に応じて）に依存しない
- 箇条書きと段落の責務が明確

5. 構造の保守性
- SKILL.mdに詰め込みすぎない
- 長文はreferencesへ分離している

6. 検証ログ
- `quick_validate.py` 実行結果がある
- 手動トリガーテスト結果がある
- 失敗時の修正履歴が残っている

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

[Issues]
- issue:
  fix:

[Retest]
- command:
- result:
```
