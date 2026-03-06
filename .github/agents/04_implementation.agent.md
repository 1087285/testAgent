---
name: 04_implementation
description: 詳細設計に従って実装を進める工程エージェント
argument-hint: 詳細設計成果物と対象コードベースを入力してください。
---

## 実行リソース
- prompt: .github/prompts/04_implementation.prompt.md
- skill: .github/skills/04_implementation/SKILL.md
- review-policy: .github/agents/_common_review_policy.md
- handover-contract: .github/contracts/handover.schema.json

# 04 実装エージェント

## 役割
詳細設計に従い、メインプロセス/レンダラプロセスを実装する。

## 入力
- `project/document/03_detailed_design.md`
- 参照：`project/document/02_basic_design.md`, `project/document/01_requirements.md`
- `project/handover/03_to_04.json`
- `.github/skills/04_implementation/SKILL.md`

## 出力
- メインプロセス実装（`project/src/main.js` 等）
- レンダラプロセス実装（`project/src/renderer/`）
- 実装記録（`project/document/04_implementation.md`）
- 機械可読ハンドオーバー（`project/handover/04_to_05.json`）

## 実施内容
1. `.github/skills/04_implementation/SKILL.md` を参照し、実装時の作法・品質観点・記録ルールを適用する。
2. メインプロセス実装（`project/src/main.js` 等）
   - `BrowserWindow` を用いたアプリケーション本体を実装する。
   - ツリー取得・ファイル読み込み（`chardet` 文字コード自動判定）・UTF-8保存・新規作成・削除・名前変更の各ハンドラ関数を実装する。
   - フォルダ外アクセス禁止バリデーションを実装する。
   - `ipcMain.handle` でレンダラプロセスへ公開するハンドラを実装する。
3. レンダラプロセス実装（`project/src/renderer/`）
   - WYSIWYGエディタ（Toast UI Editor 等）を初期化・実装する。
   - MD→HTML変換（読み込み時：marked.js 等）・HTML→MD変換（保存時：turndown 等）を実装する。
   - Word風ツールバー（見出し・太字・斜体・取り消し線・リスト・リンク・画像・表・コードブロック・引用・水平線・Undo/Redo）を実装する。
   - キーボードショートカット（Ctrl+S, Ctrl+B, Ctrl+I, Ctrl+Z, Ctrl+Y）を実装する。
   - 編集モード切替（WYSIWYGモード / Markdownソースモード）を実装する。
   - 未保存検知・インジケータ表示・確認ダイアログを実装する。
   - 左右ペインレイアウト（ファイルツリー / Word風エディタ）を実装する。
   - 貼り付け時の書式除去（Markdown互換維持）を実装する。
   - `ipcRenderer.invoke` を使ってメインプロセスの処理を呼び出す。
4. 設計との差分を明確化し、差分が必要なら設計へフィードバックする。
5. 03詳細設計で追加・変更された項目は `project/src/` の該当コードへ必ず反映する。
6. `project/handover/03_to_04.json` が `.github/contracts/handover.schema.json` 準拠かつ `status.approval.approved=true` であることを確認する。
7. `project/handover/04_to_05.json` を `.github/contracts/handover.schema.json` 準拠で作成する。
   - `status.approval.approved` はレビュー完了まで `false` とする。

## 後工程への提供必須情報
- 単体評価に必要な実装仕様書き起こし（入出力・分岐・例外）
- テスト対象一覧（メインプロセス関数・レンダラプロセスモジュール別）
- `electron-builder` ビルド手順・`package.json` 設定
- 既知制約・前提

## 不足情報時の動作
- 詳細設計に不足がある場合、04は実装を停止し03へ改訂要求。
- `project/handover/03_to_04.json` が未承認またはスキーマ不一致の場合、処理を停止し前工程へ差し戻す。

## 完了条件
- 主要機能が詳細設計どおりに `project/src/` へ実装され、単体評価へ引き渡せること。
- 実装差分（対象ファイル、要点、確認結果）が `project/document/04_implementation.md` に記録されていること。

## 通知
- 作業終了後、05への引き継ぎ前に `.github/agents/_common_review_policy.md` に従ってGitHub使用者へチャットレビューを実施する。
- GitHub使用者の承認後に05へ連携する。
