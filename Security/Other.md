# その他 Security 関連のサービス

最終編集日： 2025/9/27

## Organization Policy（組織ポリシー）

* Google Cloud における最上位リソースの「組織」からその配下リソースに特定の設定や制限を強制させることができるサービス
* コンプライアンス準拠を徹底することができる

* よくあるケース
  * SAや認証認可に関する制約
  * VPC等のネットワーク関連の制約
  * ロケーションなどリソース全体の制約

* ユースケースと設定値例
  | ユースケース | 設定値 |
  | :--- | :--- |
  | SA キーの利用を禁止したい | `iam.disableServiceAccountKeyCreation` |
  | デフォルト SA を無効化したい | `iam.automaticIamGrantsForDefaultServiceAccounts` |
  | VPC Peering の接続を一部に制限したい | `constraints/compute.restrictVpcPeering` |
  | 共有 VPC のサブネット払い出しを一部に制限したい | `constraints/compute.restrictSharedVpcSubnetworks`|
  | リソースのロケーションを限定したい | `constraints/gcp.resourceLocations` |

## Container Analytics

* Artifact Registry に格納されたコンテナの脆弱性スキャンを提供するサービス
* Google Cloud の DevSevOps への取り組みとして非常に重要なポイント

## Binary Authorization

* Artifact Registry がホストするコンテナに署名をすることで、GKE や Cloud Run にデプロイできるコンテナイメージを制御できるサービス
* Container Analytics 同様、Google Cloud の DevSecOps への取り組みとして非常に重要なポイント

* 利用されるケース
  * 本番環境で不正なコンテナイメージを実行させないように制限したい
  * 単体テストなどをクリアしていないコンテナイメージをデプロイできないようにしたい

【署名プロセス】
![alt text](./image/image2.png)

## Confidential VMs

* Compute Engine VM の一種で、使用中はメモリ内データを常に暗号化し、エンドツーエンドの暗号化とデータの保護を保証
* 機密データを取り扱うワークロードに最適
* AMD Secure Encrypted Virtualization（SEV）を搭載した AMD EPYC プロセッサでのみ動作する点は注意が必要

## Shielded VM

* Compute Engine のセキュリティオプションの1つ
* インスタンスがブートレベルまたはカーネルレベルのマルウェアやルートキットによって改ざんされていないことを保証するもの
  * セキュアブート
  * 仮想トラステッド プラットフォーム モジュール（vTPM）対応のメジャード ブート
  * 整合性モニタリング

## Private Google Access

* 内部 IP アドレスしか持たない GCE インスタンスが Google API へアクセスする場合、Private Google Access を利用することで内部経路を利用したアクセスが可能になる

## Packet Mirroring

* VPC ネットワークへ到達したトラフィックを複製し、フォレンジック用に転送するサービス
* ペイロードとヘッダーを含むすべてのトラフィックとパケットをキャプチャする
* トラフィックを複製することのメリット
  * IDS（Intrusion Detection System）等に連携して持続型の脅威を検出する
  * パケットを検査して異常なペイロードや、様々なベクトルの脅威を検出するきっかけを作る

## Certificate Authority Service（CAS）

* プライベート 認証局を Google Cloud 内に構築し、管理と運用の自動化を行うサービス
* 既存のプライベート認証局と比べて、大きく有利な点がある
  * CA をグループ化できる
  * CA のローテーションが容易
  * エンタープライズのコンプライアンス要件を満たす監査基準
    * ISO 27001、27017、27018、SOC1、SOC2、SOC3、BSI C5、PCI、FedRAMP 監査適合
    * FIPS 140-2 レベル 3 で検証された秘密鍵保護に Google Cloud HSM をデフォルトで使用

* CAS がサポートする証明書の種類
  | 証明書の種類 | 説明 |
  | ---- | ---- |
  | クライアント証明書 | サーバーに接続する**利用者やデバイスの身元**を証明します。 |
  | サーバ証明書 | 利用者に対して**ウェブサイト（サーバー）の身元**を証明し、通信を暗号化します。(SSL/TLS証明書) |
  | mTLS 証明書 | サーバーとクライアントが**お互いの身元を相互に確認**するために利用します。（クライアント/サーバ証明書の両方を使用） |
  | Code Sign | ソフトウェアやコードの**作者が正当であることと、改ざんされていないこと**を証明します。 |
  | e-mail Protection | メールの**送信者が正当であることの証明（署名）と、メール内容の暗号化**を行います。(S/MIME証明書) |