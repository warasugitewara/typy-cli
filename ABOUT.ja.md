# typy-cli について

## 概要
typy-cli は、ターミナル上でモンキータイプのようなタイピング練習ができるRustツールです。

## このフォークについて

このリポジトリは、元の[Pazl27/typy-cli](https://github.com/Pazl27/typy-cli)をフォークしたものです。

### 改変点

#### 修正した問題
- **Windows環境での二重入力問題を解決**
  - Windows Terminal、PowerShell、nushellで、入力が二重に反応していた問題を修正しました
  - 原因：crossterm の `KeyEvent` で `Press` 以外のイベント（Release など）も処理されていた

#### 実装内容
1. **キーイベントフィルタリング** (`src/terminal/game.rs`)
   - `KeyEventKind::Press` のみを処理するようフィルタリング
   - 他のキーイベント種別（Release、Repeat）は無視

2. **出力バッファ管理** (`src/terminal/keyboard.rs`)
   - `handle_correct_char()`
   - `handle_incorrect_char()` 
   - `add_incorrect_char()`
   に `stdout.flush()` を追加して、出力のバッファリング問題を改善

## クレジット

### オリジナル作成者
- **Pazl27** - [typy-cli](https://github.com/Pazl27/typy-cli)

このフォークはPazl27の元のプロジェクトに対してバグ修正を行ったものです。

## ライセンス
オリジナルプロジェクトのライセンスに従います。

## 使用方法

### インストール
```bash
cargo install --git "https://github.com/[ユーザー名]/typy-cli.git"
```

### 実行
```bash
typy              # 30秒のデフォルトゲーム
typy -t 60        # 60秒ゲーム
typy -c           # 設定ファイル作成・編集
typy --stats      # 統計表示
```

## 動作確認環境
- Windows 11
- Windows Terminal
- PowerShell 7
- Nushell
- WezTerm
- Rust 1.93.0

## 報告事項
このバージョンでWindows環境での二重入力問題が解決されました。
その他の問題や改善提案がある場合は、Issueを作成してください。
