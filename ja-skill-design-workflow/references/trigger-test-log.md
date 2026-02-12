# トリガーテストログ

## 記録ルール

- 1テストケースを1行で記録する
- 区分は `positive` / `negative` / `ambiguous` / `boundary` の4種類
- 判定は `pass` / `fail` を使う
- `description` を変更した場合は必ず変更前後の影響を記録する

## テストケース記録テンプレート

| date | skill | category | input | expected | actual | result | fix |
|---|---|---|---|---|---|---|---|
| 2026-02-12 | example-skill | positive | 〇〇したい | 発火して処理 | 発火して処理 | pass | - |

## 期待挙動の定義

- 発火して処理する
- 発火せず他skillへ委譲する
- 発火し、短い確認質問を返して判定する

## description変更時の記録テンプレート

```text
[Skill]
- name:

[Description Diff]
- before:
- after:

[Impact]
- newly_triggered:
- no_longer_triggered:
- unchanged_core_cases:

[Retest Summary]
- positive:
- negative:
- ambiguous:
- boundary:
```
