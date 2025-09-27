# その他 Security 関連のサービス

最終編集日： 2025/9/27

## Organization Policy（組織ポリシー）

* Google Cloud における最上位リソースの「組織」からその配下リソースに特定の設定や制限を強制させることができるサービス
* コンプライアンス準拠を徹底することができる

* よくあるケース
  * SAや認証認可に関する制約
  * VPC等のネットワーク関連の制約
  * ロケーションなどリソース全体の制約
    | ユースケース | 設定値 |
    | :--- | :--- |
    | SA キーの利用を禁止したい | `iam.disableServiceAccountKeyCreation` |
    | デフォルト SA を無効化したい | `iam.automaticIamGrantsForDefaultServiceAccounts` |
    | VPC Peering の接続を一部に制限したい | `constraints/compute.restrictVpcPeering` |
    | 共有 VPC のサブネット払い出しを一部に制限したい | `constraints/compute.restrictSharedVpcSubnetworks`|
    | リソースのロケーションを限定したい | `constraints/gcp.resourceLocations` |