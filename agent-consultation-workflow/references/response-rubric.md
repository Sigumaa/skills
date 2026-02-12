# 回答評価ルーブリック

## 目的

外部AIから得た回答を比較可能な形で評価し、実装判断を安定させる。

## 評価軸

1. 結論の明確さ
- 1文で判断が明示されているか

2. 根拠の妥当性
- 背景・制約に沿った理由になっているか

3. 代替案の実用性
- 代替案が実際に実行可能か

4. リスクの具体性
- 技術/運用リスクが具体的に示されているか

5. 信頼度の整合性
- confidence と根拠の強さが一致しているか

## 判定テンプレート

```text
[Source]
- agent:
- timestamp:

[Evaluation]
- clarity: pass/fail
- rationale: pass/fail
- alternatives: pass/fail
- risks: pass/fail
- confidence: pass/fail

[Adopt]
- decision:
- reason:
- confidence:

[Open Risks]
- risk:
- mitigation:
```

## 採用基準

- `pass` が4項目以上
- `conclusion` と `next_action` が矛盾しない
- リスクに具体的な緩和策がある
