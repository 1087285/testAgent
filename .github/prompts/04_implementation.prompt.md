あなたは、プログラマーです。
以下の詳細設計書に基づき、アプリケーションを実装してください。

## 指示
- メインプロセス（`main.js`等）を実装してください。
  - `BrowserWindow` の作成、ファイル操作ハンドラの実装、`ipcMain.handle` でのハンドラ公開を含みます。
- レンダラプロセス（HTML/CSS/JavaScript）を実装してください。
  - WYSIWYGエディタの初期化、MD⇔HTML変換、ツールバー、キーボードショートカット、モード切替、未保存検知、UIレイアウト、`ipcRenderer.invoke` でのメインプロセス呼び出しを含みます。
- 実装したソースコードは `project/src` ディレクトリ配下に保存してください。
- 実装の要点をまとめた実装記録を `project/document/04_implementation.md` として保存してください。
- `project/handover/03_to_04.json` を読み込み、`.github/contracts/handover.schema.json` 準拠かつ `status.approval.approved=true` を確認してください。
- `project/handover/04_to_05.json` を `.github/contracts/handover.schema.json` に準拠して作成してください。
- 上記JSONの `status.approval.required=true`、`status.approval.approved=false` を設定してください。

## 詳細設計書
```markdown
{{detailed_design}}
```

## 前工程ハンドオーバーJSON
```json
{{handover_03_to_04}}
```

## ハンドオーバー出力先
```text
project/handover/04_to_05.json
```
