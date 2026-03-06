あなたは、テストエンジニアです。
以下の基本設計書と単体評価結果に基づき、結合評価を実施してください。

## 指示
- メインプロセス ⇔ レンダラプロセス（IPC）間の連携を評価してください（`ipcRenderer.invoke` 呼び出し、戻り値、エラー処理）。
- ファイル操作（ツリー表示→選択→読み込み→表示→編集→保存）の結合フローを評価してください。
- WYSIWYG編集（MD読み込み→HTML変換→編集→MD変換→保存）の結合フローを評価してください。
- 未保存検知、モード切替、確認ダイアログの連携動作を評価してください。
- 評価項目、結果、備考を記載した結合評価結果書を `project/document/06_integration_test.md` として保存してください。
- `project/handover/05_to_06.json` を読み込み、`.github/contracts/handover.schema.json` 準拠かつ `status.approval.approved=true` を確認してください。
- `project/handover/06_to_07.json` を `.github/contracts/handover.schema.json` に準拠して作成してください。
- 上記JSONの `status.approval.required=true`、`status.approval.approved=false` を設定してください。

## 基本設計書
```markdown
{{basic_design}}
```

## 単体評価結果
```markdown
{{unit_test_report}}
```

## 前工程ハンドオーバーJSON
```json
{{handover_05_to_06}}
```

## ハンドオーバー出力先
```text
project/handover/06_to_07.json
```
