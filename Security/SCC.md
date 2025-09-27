# Security Command Center（SCC）

最終編集日： 2025/9/27

## 概要

Google Cloud 上で使用しているサービスの脆弱性や脅威となりうる設定を検知することができるサービス

* 検知された脆弱性や脅威は、Google Cloud のダッシュボードに表示したり Pub/Sub にメッセージをパブリッシュすることができる
* SCC は Google Cloud の組織単位で有効にできるサービスなので、Google Cloud プロジェクトのみを使用しているユーザーは使用できない

## 機能

### Security Health Analytics

* Google Cloud 内の脆弱性を検知する、マネージド脆弱性スキャン機能

* 検知可能な対象
  * 一般的な脆弱性（CIS Benchmarkに基づく）
  * 明らかな構成ミス（Firewallに過剰な穴がある、IAM権限が余剰である、等）

* 対応しているプロダクト
  * Cloud Monitoring/Logging
  * Compute Engine/GKE
  * Cloud Storage
  * Cloud SQL
  * Cloud IAM
  * Cloud KMS
  * Cloud DNS

* スキャンモード

    | 用語 | 説明 |
    | ---- | ---- |
    | バッチスキャン | 	1日に2回以上定期実行する。<br>12時間毎 or 6時間毎に実行を選択する。 |
    | リアルタイムスキャン | リソース構成の変更が発生する度にリアルタイムに実行する。 |
    | 混合モード | 	リアルタイムスキャンでは対応できないリソースの場合、例外的にバッチスキャンを実行する。 |



