あなたは、ソフトウェア設計者です。
以下の基本設計書に基づき、アプリケーションの詳細設計を行ってください。

## 指示
- メインプロセス（`main.js`等）の各関数を関数レベルで定義してください（`ipcMain.handle` で公開するハンドラ、引数、戻り値、エラー処理を含む）。
- レンダラプロセス（`renderer.js`等）の各モジュールを定義してください（WYSIWYGエディタの初期化・操作、MD⇔HTML変換、ツールバー操作、キーボードショートカット、状態管理等）。
- IPCインターフェース（チャネル名、引数、戻り値、エラー処理）を一覧表化してください。
- 異常系仕様（パス不正、ファイル未存在、読み取り失敗、保存失敗）を定義してください。
- `electron-builder` のビルド設定要件を定義してください。
- 作成した詳細設計書は、`project/document/03_detailed_design.md` として保存してください。
- `project/handover/02_to_03.json` を読み込み、`.github/contracts/handover.schema.json` 準拠かつ `status.approval.approved=true` を確認してください。
- `project/handover/03_to_04.json` を `.github/contracts/handover.schema.json` に準拠して作成してください。
- 上記JSONの `status.approval.required=true`、`status.approval.approved=false` を設定してください。

## 基本設計書
```markdown
{{basic_design}}
```

## 前工程ハンドオーバーJSON
```json
{{handover_02_to_03}}
```

## ハンドオーバー出力先
```text
project/handover/03_to_04.json
```
