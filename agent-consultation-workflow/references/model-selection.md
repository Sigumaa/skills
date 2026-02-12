# Copilot モデル選定ガイド

## 現在選べるモデル（この環境で確認）

- `claude-sonnet-4.5`
- `claude-haiku-4.5`
- `claude-opus-4.6`
- `claude-opus-4.6-fast`
- `claude-opus-4.5`
- `claude-sonnet-4`
- `gemini-3-pro-preview`
- `gpt-5.3-codex`
- `gpt-5.2-codex`
- `gpt-5.2`
- `gpt-5.1-codex-max`
- `gpt-5.1-codex`
- `gpt-5.1`
- `gpt-5`
- `gpt-5.1-codex-mini`
- `gpt-5-mini`
- `gpt-4.1`

## 選定ルール

1. 深い設計比較・難しい意思決定
- primary: `gpt-5.3-codex` または `claude-opus-4.6`
- challenger: `claude-sonnet-4.5` または `gpt-5.2-codex`

2. 実装寄りの技術判断
- primary: `gpt-5.2-codex` または `gpt-5.1-codex`
- challenger: `claude-sonnet-4.5`

3. 速度重視の一次評価
- primary: `gpt-5-mini` または `claude-haiku-4.5`
- challenger: 必要時のみ追加

4. 不確実性が高い場合
- 必ず2モデルで同一照会文を実行し、差分比較する

## 実行テンプレート

```bash
copilot -s --model <model_name> --allow-all-tools --add-dir <repo_path> -p "<query>"
```

## 比較時のルール

- 同じ背景情報と同じ質問文を使う
- 回答形式を固定する
- 結論が割れた場合は、根拠の具体性が高い方を優先する
