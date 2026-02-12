---
name: go-dev-workflow
description: Goプロジェクトの新規立ち上げと日常開発フローを標準化するスキル。go mod initによる初期化、ディレクトリ構成、実装、依存整理、go fmt/go vet/go testによる検証、コミット前チェックまでを案内する。Go言語で新規開発を始めるとき、既存Goリポジトリへ機能追加するとき、品質ゲートを明確化したいときに使用する。言語非依存の設計相談のみの依頼や、Go以外の実装依頼には使用しない。
---

# Go 開発手順

## Overview

Go開発の開始から日常運用まで、再現性の高い手順で進める。  
依頼を受けたら「新規作成」か「既存更新」かを先に判定し、該当フローを実行する。

## ワークフロー判定

- `go.mod` が存在しない: 新規作成フローを実行する
- `go.mod` が存在する: 既存更新フローを実行する

## 新規作成フロー

1. モジュール名を決める
- 例: `github.com/<org>/<repo>` または社内規約のパス

2. プロジェクトを初期化する
```bash
go mod init <module-path>
```

3. 最小構成で起動確認する
```bash
mkdir -p cmd/app
cat > cmd/app/main.go <<'EOF'
package main

import "fmt"

func main() {
	fmt.Println("hello")
}
EOF
go run ./cmd/app
```

4. 基本ディレクトリ方針を整える
- `cmd/<app>`: エントリポイント
- `internal/<domain>`: 非公開実装
- `pkg/<name>`: 外部公開を意図した共通パッケージ（必要な場合のみ）

## 既存更新フロー

1. 現状を把握する
- `go.mod`, `go.sum`, `cmd/`, `internal/`, `pkg/`, 既存テストを確認する

2. 変更単位を分割する
- 1機能ごとに小さく実装し、同時に `*_test.go` を追加する

3. 検証ループを回す
```bash
go fmt ./...
go test ./...
go vet ./...
```

4. 依存を整理する
- 依存を追加・削除したら必ず実行する
```bash
go mod tidy
```

## 実装ルール

- エラーは `fmt.Errorf("...: %w", err)` でラップする
- 判定は `errors.Is` / `errors.As` を優先する
- `panic` はプロセス継続不能時に限定する
- 公開識別子には GoDoc コメントを付ける
- 命名は短く明確にし、パッケージ名は小文字で統一する

## コミット前チェック

以下を順に実行し、失敗を解消してからコミットする。

```bash
go fmt ./...
go test ./...
go vet ./...
go mod tidy
git diff -- go.mod go.sum
```

必要に応じて追加で実行する。

```bash
go test -race ./...
go test -cover ./...
```

## 依頼への返答方針

- 実行したコマンドを順序付きで報告する
- 生成・変更したファイルを明示する
- テスト結果（成功/失敗、失敗時ログ要点）を簡潔に添える
- 未実行項目がある場合は理由を明示する
