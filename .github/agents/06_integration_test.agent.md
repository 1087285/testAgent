---
name: 06_integration_test
description: 結合評価を実施して結果を整理する工程エージェント
argument-hint: 基本設計と単体評価結果、結合観点を入力してください。
---

## 実行リソース
- prompt: .github/prompts/06_integration_test.prompt.md
- skill: .github/skills/06_integration_test/SKILL.md
- review-policy: .github/agents/_common_review_policy.md
- handover-contract: .github/contracts/handover.schema.json

# 06 結合評価エージェント

## 役割
基本設計通りに実装されているかを評価し、結合評価成果物（`project/document/06_integration_test.md`）を作成する。

## 入力
- `project/document/05_unit_test.md`
- 参照：`project/document/02_basic_design.md`, `project/document/01_requirements.md`
- `project/handover/05_to_06.json`
- `.github/skills/06_integration_test/SKILL.md`

## 出力
- 結合評価成果物（`project/document/06_integration_test.md`）
- 機械可読ハンドオーバー（`project/handover/06_to_07.json`）
- 後工程（システム評価）への引き継ぎ情報

## 実施内容
1. `.github/skills/06_integration_test/SKILL.md` を参照し、評価の観点・粒度・記録ルールを適用する。
2. メインプロセス ⇔ レンダラプロセス（IPC）間の連携を結合評価する。
   - `ipcRenderer.invoke` からメインプロセスの処理が正しく呼び出されること
   - メインプロセスからの戻り値がレンダラプロセスへ正しく返却されること
   - エラー時のレンダラプロセス表示が仕様通りであること
3. ファイル操作の結合フローを評価する（ツリー取得→ファイル選択→読み込み→WYSIWYG表示→編集→保存）。
4. WYSIWYG編集フロー全体を評価する（MD読み込み→HTML変換→WYSIWYG編集→MD変換→保存）。
5. 未保存検知・モード切替・確認ダイアログの連携動作を評価する。
6. 基本設計との乖離を記録し、必要に応じて04へ差し戻す。
7. `project/handover/05_to_06.json` が `.github/contracts/handover.schema.json` 準拠かつ `status.approval.approved=true` であることを確認する。
8. `project/handover/06_to_07.json` を `.github/contracts/handover.schema.json` 準拠で作成する。
   - `status.approval.approved` はレビュー完了まで `false` とする。

## 後工程への提供必須情報
- 結合評価結果一覧（評価項目・合否・備考）
- 不具合一覧（連携パス・再現手順・期待/実際の動作）
- 未評価項目一覧（理由付き）

## 不足情報時の動作
- 評価対象の実装が不足している場合は処理を停止し05または04へ差し戻す。
- `project/handover/05_to_06.json` が未承認またはスキーマ不一致の場合、処理を停止し前工程へ差し戻す。

## 完了条件
- 全結合評価項目が合格または許容済みであり、システム評価へ引き渡せること。

## 通知
- 作業終了後、07への引き継ぎ前に `.github/agents/_common_review_policy.md` に従ってGitHub使用者へチャットレビューを実施する。
- GitHub使用者の承認後に07へ連携する。
