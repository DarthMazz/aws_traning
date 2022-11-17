・テキストの閲覧は、https://evantage.gilmoreglobal.com/ または https://online.vitalsource.com/ で閲覧できます。
テキストの閲覧には、https://evantage.gilmoreglobal.com/ または
https://online.vitalsource.com/ にサインインする必要があります。
これらのサイトにアカウントがない場合は、アカウントを作成してください。
テキストは、本日の研修終了後 2 年間閲覧可能です。
テキストの閲覧については、トレーニング開始後改めてご案内します。
Mitsuru Nishikawa から全員へ: 9:30 AM
https://bit.ly/3NGuuEK
Mitsuru Nishikawa から全員へ: 9:34 AM

音が聞こえない場合は以下の URL p.27 をご確認ください
https://a.co/2RkfyGA

自己紹介
お名前：松本義高
現在のロール：開発
コースに期待すること：AWS にまずは慣れること
AWS のご経験：未経験

- AWS 紹介

  - クラウドコンピューティングとは

    - オンデマンドなサービスアクセス
    - 必要に応じてコンピューティングリソースをプロビジョニング
    - 従量課金

  - クラウドコンピューティングの利点

    - 従量課金
    - スケールメリット
    - キャパシティの予測が不要
    - スピードと俊敏性が向上
    - コスト削減
    - 数分でデプロイ

  - サービス

    - AWS グローバルインフラストラクチャ
      - リージョン
        - 地理的ロケーション
        - リージョンの選択
          以下優先順位順
          - データコンプライアンス（重要）
          - レイテンシー（重要）
          - 料金
          - 利用できるサービス
      - アベイラビリティゾーン（AZ）
        - １つ以上のデータセンターで構成される
        - 耐障害性のために複数のデータセンターが存在する（可用性の向上）
      - エッジロケーション
        - CloudFront（CDN）
    - サービス管理
      いづれも全て API でアクセスする

      - AWS マネーメントコンソる
      - AWS CLI
      - AWS SDK

    - セキュリティ
      - 責任共有モデル
        - クラウド内のセキュリティについて責任はユーザ側
          - OS, ファイアウォール, データ暗号化など
        - クラウドのセキュリティについて責任は AWS
          - AWS グローバルインフラストラクチャ
          - AWS Lambda のセキュリティパッチは AWS 側の責任
    - IAM
      - IAM とは認証と認可
      - 対象はユーザとサービス
      - 特徴
        - グローバル
        - 無料
        - ID フェデレーション（ID 連携）
        - MFA
      - AWS ルートユーザ
        - AWS アカウントの作成（メールアドレス/パスワードでログインする）
        - 日常的には使わない
        - ルートユーザのアクセスキーを無効にする
        - 管理者ユーザを作成して操作する
      - IAM ユーザ
        - AWS にアクセスする人毎に IAM ユーザを作成する
      - IAM ポリシー
        - アクセう許可／拒否
        - JSON で記述する
        - ベストプラクティスは最小権限の原則に従う
      - IAM グループ
        - ベストプラクティスは IAM グループに行う
      - IAM ロール
        - 一時的セキュリティ認証情報（AssumeRole）
        - 一時的にアクセスのために人またはサービスが引き受けるアイデンティティ
      - MFA（多要素認証）
        - ハードウェアを利用した仮想 MFA

  https://237000222259.signin.aws.amazon.com/console

- AWS コンピューティング

  - EC2
  - ECS
  - EKS
  - Fargate
  - Lambda
  - Compute as a Service (Cass)
    - Amazon Elastic Compute Cloud (EC2)
      - サイズ変更可能なコンピューティングキャパティ
      - 数分でプロビジョニング
      - 従量課金
    - インスタンスタイプ
      - 汎用 (M)
      - コンピューティング最適化 (C)
      - メモリ最適化 (R)
      - 高速コンピューティング (P)
      - ストレージ最適化 (D)
    - 料金
      - AWS 無料枠
      - オンデマンド
      - スポットインスタンス
      - Savings Plans
      - リザーブドインスタンス
      - Dedicated Hosts
  - 新 UI
    https://bit.ly/3RyPBJl

  - EC2
    https://docs.aws.amazon.com/ja_jp/ec2/
    https://aws.amazon.com/jp/premiumsupport/knowledge-center/ec2-instance-connect-troubleshooting/
  - AWS トレーニング
    http://aws.amazon.com/training/
  -

- AWS ネットワーキング

  - VPC
    - アベイラビリティゾーン毎にサブネットを構成
      - パブリックサブネット（インターネットからアクセス化）
        10.0.0.0/24, 10.0.1.0/24
      - プライベートサブネット
        10.0.2.0/24, 10.0.2.0/24
  - サブネット
    - インターネットゲートウェイ経由のアクセスはパブリックサブネットのみアクセスする
    - NAT ゲートウェイは外向きの GW
  - ルートテーブル
    - インターネットゲートウェイと関連づけられているサブネット->パブリックサブネット
  - ネットワーク ACL
    - 保護対象はサブネット
    - ステートレス（リクエストとレスポンスを管理していない）
      - インバウンド／アウトバウンド毎に設定する
  - セキュリティグループ
    - 保護対象はインスタンス
    - ステートフル
      - インバウンドは全て拒否
  - ホストベースのファイアウォール

  全てのレイヤーでセキュリティを設定する（保護する）
  AWS のログは既定では全てオフ

  - ラボ 3 注意事項
    手順 3.～ 6. はスキップします。
    - NAT ゲートウェイ用の Elastic IP は、手順 9.,10.の VPC を作成 の際に割り当てられるので、この手順は不要です。
      画面表示の変更
      手順 8. [Create VPC] は、[VPC を作成]です。
      手順 9.
      ・作成するリソース：[VPC など] を選択
      手順 13. VIRTUAL PRIVATE CLOUD セクションを探し、VPC をクリックします。
      => 仮想プライベートクラウド セクションを探し、お使いの VPC をクリックします。
      手順 17. VIRTUAL PRIVATE CLOUD セクションを探し、サブネットを選択します。
      => 仮想プライベートクラウド セクションを探し、サブネットを選択します。
      手順 33. [VIRTUAL PRIVATE CLOUD] の [ルートテーブル] をクリックします。
      => [仮想プライベートクラウド] の [ルートテーブル] をクリックします。
      手順 48. の VPC の指定のところで、最初に表示されている VPC は Default VPC となっていて、Lab VPC ではないため、X で選択を解除してから、Lab VPC を選択します。
      ラボ 3 新 UI での EC2 インスタンス作成手順
      https://bit.ly/3M3bfEw

  vpc-042921e60bb6e96bd

- AWS ストレージ

  - ストレージタイプ
    - ブロックタイプ (EBS)
    - ファイルタイプ (EFS=Linux 用)
    - オブジェクトタイプ (S3)
      - セキュリティ
        - IAM ポリシー
        - バケットポリシー
        - S3 アクセスコントロール
        - S3 の暗号化
      - バージョニング
        - デフォルト無効
        - バケットレベルで有効化
        - アップロードするたびに保持

  employee-photo-bucket-ym-9999

- データベース

  - タイプ
    - フルマネージド型
    - 大規模環境
  - リレーショナルデータベース
    - SQL
    - 広く普及している
    - トランザクション
  - Amazon DynamoDB
    - フルマネージド型
    - キーバリューデータベース
    - 高いスケーラビリティ

- モニタリング、ロードバランシングおよびスケーリング

  - Amazon CloudWatch
    - AWS とオンプレミスを確認
  - Amazon CloudWatch メトリクス
  - Amazon CloudWatch Logs

  - Elastic LoadBalancer
    - ALB http/https
      - TLS オフロード
        - TSL で受信して配下には HTTP で通信する
    - NLB tcp/udp/tls
  - Amazon EC2 Auto Scaling
    - 対象障害性向上
    - アプリケーションの可用性の向上
    - 起動テンプレート
    - Amazon EC2 Auto Scaling グループ
      - 最小容量
      - 希望する容量
      - 最大容量
    - スケーリングポリシー
      - ターゲット追跡スケーリングポリシー
      - シンプルスケーリングポリシー
      - ステップスケーリングポリシー

- コースまとめ

最終的なラボアプリケーション

質問
エッジロケーションは同じリージョン内に限定することは可能でしょうか？

AWS Hands on Beginers
https://pages.awscloud.com/event_JAPAN_Ondemand_Hands-on-for-Beginners-1st-Step_LP.html

https://d1.awsstatic.com/ja_JP/training-and-certification/docs-sa-assoc/AWS-Certified-Solutions-Architect-Associate_Exam-Guide.pdf

https://aws.amazon.com/jp/events/aws-event-resource/archive/
