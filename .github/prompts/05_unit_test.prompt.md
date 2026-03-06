あなたは、テストエンジニアです。
以下の詳細設計書と実装コードに基づき、単体評価を実施してください。

## 指示
- メインプロセスの各関数（`ipcMain.handle` ハンドラ含む）の単体評価を行ってください（正常系・異常系）。
- レンダラプロセスの各モジュール（WYSIWYGエディタ、MD⇔HTML変換、ツールバー、ショートカット等）の単体評価を行ってください。
- IPCインターフェースの入出力仕様を確認してください。
- 評価項目、結果、備考を記載した単体評価結果書を `project/document/05_unit_test.md` として保存してください。
- `project/handover/04_to_05.json` を読み込み、`.github/contracts/handover.schema.json` 準拠かつ `status.approval.approved=true` を確認してください。
- `project/handover/05_to_06.json` を `.github/contracts/handover.schema.json` に準拠して作成してください。
- 上記JSONの `status.approval.required=true`、`status.approval.approved=false` を設定してください。

## 詳細設計書
```markdown
{{detailed_design}}
```

## 実装コード
```
{{source_code}}
```

## 前工程ハンドオーバーJSON
```json
{{handover_04_to_05}}
```

## ハンドオーバー出力先
```text
project/handover/05_to_06.json
```
