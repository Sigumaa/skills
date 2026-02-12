# Copilot モデル選定ガイド

## 現在選べるモデル（この環境で確認）

- `claude-sonnet-4.5`
- `claude-haiku-4.5`
- `claude-opus-4.6`
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

## この環境の運用前提

- 既定は Codex 系最新モデルを優先する（例: `gpt-5.3-codex`）
- Codexで解決しない場合は `claude-opus-4.6` を優先フォールバックにする
- `claude-opus-4.6-fast` は現状利用しない（プラン非対応）

## 選定ルール

1. 深い設計比較・難しい意思決定
- primary: `gpt-5.3-codex`
- fallback: `claude-opus-4.6`
- challenger: `gpt-5.2-codex` または `claude-sonnet-4.5`

2. 実装寄りの技術判断
- primary: `gpt-5.2-codex` または `gpt-5.1-codex`
- fallback: `claude-opus-4.6`
- challenger: `claude-sonnet-4.5` または `gpt-5-mini`

3. 速度重視の一次評価
- primary: `gpt-5-mini` または `claude-haiku-4.5`
- challenger: 必要時のみ追加
- 重要判断に進む前に `gpt-5.3-codex` か `claude-opus-4.6` で再確認する

4. 不確実性が高い場合
- 必ず2モデルで同一照会文を実行し、差分比較する

5. CodexからOpusへ切替える条件
- 結論が曖昧で confidence が `low` のまま
- 同じ制約で2回以上照会しても改善しない
- 代替案は出るが採用判断に必要な根拠が不足している

## 実行テンプレート

```bash
copilot -s --model <model_name> --allow-all-tools --add-dir <repo_path> -p "<query>"
```

## 比較時のルール

- 同じ背景情報と同じ質問文を使う
- 回答形式を固定する
- 結論が割れた場合は、根拠の具体性が高い方を優先する
- 最終判断時は採用モデル名を記録する
