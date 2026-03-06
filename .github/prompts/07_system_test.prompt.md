あなたは、品質保証担当者です。
以下の要件定義書と結合評価結果に基づき、システム評価を実施してください。

## 指示
- 要件定義書に記載されたすべての要件を網羅的に評価してください。
- Word風WYSIWYGエディタとしての実使用シナリオを評価してください。
- 配布形式（`electron-builder` で生成された .exe / インストーラ）の動作を Windows 10/11 で確認してください。
- 正常系・異常系の受入条件が満たされているかを確認してください。
- 評価項目、結果、備考を記載したシステム評価結果書を `project/document/07_system_test.md` として保存してください。
- `project/handover/06_to_07.json` を読み込み、`.github/contracts/handover.schema.json` 準拠かつ `status.approval.approved=true` を確認してください。
- `project/handover/07_to_08.json` を `.github/contracts/handover.schema.json` に準拠して作成してください。
- 上記JSONの `status.approval.required=true`、`status.approval.approved=false` を設定してください。

## 要件定義書
```markdown
{{requirements}}
```

## 結合評価結果
```markdown
{{integration_test_report}}
```

## 前工程ハンドオーバーJSON
```json
{{handover_06_to_07}}
```

## ハンドオーバー出力先
```text
project/handover/07_to_08.json
```
