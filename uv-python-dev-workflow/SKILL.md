---
name: uv-python-dev-workflow
description: uvを使ったPython開発の標準フローを提供するスキル。uv initによる初期化、仮想環境作成、依存追加、実装、ruff/mypy/pytestによる検証、ロック更新とコミット前チェックまでを一貫して案内する。新規Pythonプロジェクトを立ち上げるとき、既存プロジェクトで機能追加するとき、開発手順を統一したいときに使用する。一般的な設計相談のみの依頼や、uvを使わない前提のPython運用には使用しない。
---

# uv Python 開発手順

## Overview

uvベースで、初期化から実装・テストまでの作業を再現性高く進める。  
依頼を受けたらまず「新規プロジェクト」か「既存プロジェクト」かを判定して、対応するフローを実行する。

## フロー判定

- `pyproject.toml` がない: 新規プロジェクトフローを実行する
- `pyproject.toml` がある: 既存プロジェクトフローを実行する

## 新規プロジェクトフロー

1. 初期化する

アプリケーションなら:

```bash
uv init --app <project-name>
cd <project-name>
```

ライブラリなら:

```bash
uv init --lib <project-name>
cd <project-name>
```

2. 仮想環境を作成する

```bash
uv venv .venv
```

3. 依存を同期する

```bash
uv sync
```

4. 開発依存を追加する

```bash
uv add --dev ruff mypy pytest
```

5. 最小確認を実行する

```bash
uv run python --version
uv run pytest -q
```

## 既存プロジェクトフロー

1. 構成を確認する

- `pyproject.toml`, `uv.lock`, `src/`, `tests/` の有無を確認する
- 既存の実行コマンド（`uv run ...`）を確認する

2. 依存を同期する

```bash
uv sync
```

3. 不足する開発依存を追加する

```bash
uv add --dev ruff mypy pytest
```

## 実装フロー

1. 変更計画を小さく分割する

- 1機能ごとに実装して、同じ単位でテストを追加する

2. 依存を追加する（必要時）

```bash
uv add <package>
```

開発専用依存は:

```bash
uv add --dev <package>
```

3. 実装する

- アプリは `src/` または既存構成に合わせて実装する
- 公開APIには型ヒントを付ける
- 例外は握りつぶさず、原因が追える形で扱う

4. テストを追加する

- 追加機能ごとに `tests/` 配下へ `test_*.py` を作成する
- 正常系に加えて失敗系を1件以上含める

## 検証フロー

変更ごとに次を順に実行する。

```bash
uv run ruff format
uv run ruff check
uv run mypy
uv run pytest -q
```

必要に応じて対象を絞る。

```bash
uv run mypy src tests
uv run pytest -q tests/<target_file>.py
```

## ロックと依存更新

依存を更新したらロックを更新する。

```bash
uv lock --upgrade <package>
```

`requirements.in` / `requirements.txt` を運用しているプロジェクトでは、次も実行する。

```bash
uv pip compile requirements.in -o requirements.txt
```

## コミット前チェック

```bash
uv sync
uv run ruff format --check
uv run ruff check
uv run mypy
uv run pytest -q
git diff -- pyproject.toml uv.lock requirements.in requirements.txt
```

差分が意図どおりであることを確認してからコミットする。

## 返答方針

- 実行したコマンドを順番に示す
- 変更ファイルを明示する
- テスト結果と失敗時ログ要点を記載する
- 未実施項目がある場合は理由を明示する
