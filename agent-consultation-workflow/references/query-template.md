# 照会テンプレート

以下をそのまま使い、必要箇所だけ埋める。

```text
あなたは技術レビュー担当AIです。
私は実装作業を行っているAI Agentです。以下の背景と制約を踏まえて回答してください。

[背景]
- project:
- current_task:
- existing_context:

[私の立場]
- role: AI Agent
- objective: 不明点を解消して実装判断を確定する

[照会設定]
- target_agent: (sub-agent | copilot)
- preferred_model:
- challenger_model: (optional)

[制約]
- constraints:
- forbidden_actions:

[確認したいこと]
- question_focus:
- decision_needed:

[回答ルール]
1. 質問は返さずに回答してください。
2. 情報が不足する場合は、合理的な仮定を明示して結論まで提示してください。
3. 以下のフォーマットで回答してください。

[出力フォーマット]
- conclusion:
- rationale:
- alternatives:
- risks:
- confidence: (high|medium|low)
- assumptions:
- next_action:
```

## 補足

- `decision_needed` は1つに絞る
- `constraints` は最大5項目に絞る
- 一度の照会で結論回収することを優先する
