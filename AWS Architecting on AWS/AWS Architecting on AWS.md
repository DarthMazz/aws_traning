# 準備

- チャット環境

  - https://d2cndr8373vco9.cloudfront.net/

- コース準備 URL

  - https://arch.nijot.org

- 上記 URL でアクセスできない方向け代替 URL

  - https://main.d7vb2gd6x2u4t.amplifyapp.com/

- 学習を最適化する

- 楽しむ

# 参考

- AWS アーキテクチャアイコン

  - https://aws.amazon.com/jp/architecture/icons/

- AWS の誕生秘話: How AWS came to be

  - https://techcrunch.com/2016/07/02/andy-jassys-brief-history-of-the-genesis-of-aws/

- クラウドの特徴

  - https://aws.amazon.com/what-is-cloud-computing

- リリース回数

  - https://aws.amazon.com/jp/aws-ten-reasons/

- AWS のドキュメント

  - https://docs.aws.amazon.com/ja_jp/index.html
  - サービス別資料
    - https://aws.amazon.com/jp/aws-jp-introduction/aws-jp-webinar-service-cut/
  - AWS オンラインセミナースケジュール
  - https://aws.amazon.com/jp/about-aws/events/webinars/

- AWS への近道

  - AWS BlackBelt
  - サービス別資料
  - API ドキュメント

- グローバルインフラストラクチャ

  - https://aws.amazon.com/jp/about-aws/global-infrastructure/

- EU 一般データ保護規則

  - https://ja.wikipedia.org/wiki/EU%E4%B8%80%E8%88%AC%E3%83%87%E3%83%BC%E3%82%BF%E4%BF%9D%E8%AD%B7%E8%A6%8F%E5%89%87

- 十分性認定　データ移転禁止に例外

  - https://www.nikkei.com/article/DGKKZO45264070V20C19A5EA2000/

- リージョン別サービス
  - https://aws.amazon.com/jp/about-aws/global-infrastructure/regional-product-services/

# 概要

オンプレミス向け

- モジュール１：アーキテクチャ設計の基礎
- モジュール２：アカウントのセキュリティ
- モジュール４：コンピューティング
- モジュール３：ネットワーク１
  - ラボ２
- モジュール５：ストレージ
- モジュール６データベースサービス
  - ラボ６
- モジュール７：モニタリングとスケーリング
  - ラボ４：

クラウドネイティブ

- モジュール８：オートメーション
- モジュール９：コンテナ
- モジュール１０：ネットワーク２
- モジュール１１：サーバーレス
- モジュール１２：エッジサービス

# 自己紹介

名前：松本義高
担当業務：ソリューションサービス開発リーダ
受講目的：業務で AWS を利用したサービス開発を始める予定なので、開発に必要な知識を学びたい
AWS の経験レベル：なし（最近コンソールにログインしてアクセスしてお試しで勉強している）
嬉しかったこと：先月に金沢旅行して、美味しいものを食べてきたこと（お鮨がうまい）
ラボ環境／テキスト共にアクセス問題ありません

# モジュール１：アーキテクチャ設計の基礎

- AWS とは何か？
- クラウドリソースへのアクセスを制御するには？
- Well Architected Framework

- AWS

  - Amazon Web Services

  - システムを疎結合化し API でアクセスする方式

    - マイクロサービス化

  - オンデマンドで IT リソースを利用可能(API による操作)
  - ダイナミックに拡張可能
    - 不要になったら削除可能
  - 従量課金性

- クラウドコンピューティングの特徴

  - 固定の償却コストが変更コストに
    - two way でやり直しが効く
  - スケールによる大きなコストメリット
  - キャパシティーの予測が不要に
  - 速度と俊敏性の向上
    - 曖昧で予測不能なため、仮説を立ててすぐに確認出来る
    - まずはやってみることができる
    - リーンスタートアップ
  - データセンターの運用保守投資が不要
  - わずか数分で世界中にデプロイ

- AWS CDK

  - CloudFormation のテンプレート作成

- コンソール
  - ナビゲーションペイン
    - AWS コンソールの左側のメニュー
- サンプル CLI コマンド

  ```shell
  # CLI によるインスタンスの起動
  aws ec2 run-instances --image-id "ami-0bfb5576f775af70c" --count 1 --instance-type "t3.micro" --tag-specifications '[{"ResourceType":"instance","Tags":[{"Key":"Name","Value":"ArchDemoCLI"}]},{"ResourceType":"volume","Tags":[{"Key":"Name","Value":"ArchDemoCLI"}]}]' --region ap-northeast-1 --no-cli-pager --profile training01

  # CLI によるインスタンスの検索

  aws ec2 describe-instances --filters "Name=tag:Name,Values=ArchDemoCLI" "Name=instance-state-name,Values=running,pending"  --query "Reservations[].Instances[].InstanceId" --output text --region ap-northeast-1 --profile training01

  instanceid=$(aws ec2 describe-instances --filters "Name=tag:Name,Values=ArchDemoCLI" "Name=instance-state-name,Values=running,pending"  --query "Reservations[].Instances[].InstanceId" --output text --region ap-northeast-1 --profile training01)

  # CLI によるインスタンスの終了

  aws ec2 terminate-instances --instance-ids $instanceid --profile training01
  ```

- AWS グローバルインフラストラクチャ

  - データセンター
  - アベイラビリティゾーン
  - リージョン
  - ローカルゾーン
    - https://aws.amazon.com/jp/about-aws/global-infrastructure/localzones/locations/?nc=sn&loc=3&refid=mttc_prt_link_2

- AWS Well-Architected Framework

  - https://aws.amazon.com/jp/architecture/well-architected/
  - https://docs.aws.amazon.com/ja_jp/wellarchitected/latest/framework/welcome.html
  - Well-Architected Tool
    - レビュー管理サービス

- モジュール１振り返り

```
1. AWSを利用するメリットは？
物理的なハードウェアを用意しなくても、サービスを迅速に展開することができ、すぐに仮説を確認することが可能になること

2. AWS上のリソース操作する手段は？
ウェブブラウザを利用したコンソールによる手動操作
AWS CLI を利用したコマンドラインインターフェースからの操作
AWS SDK を利用したプログラムからの操作

3. AWSグローバルインフラストラクチャの構成要素と特徴は？
データセンター、アベイラビリティゾーン（AZ）、リージョン
ローカルリージョン、エッジロケーション
複数のデータセンターをまとめたものがAZ
AZをまとめたものがリージョン
複数のAZにリソースを配置することで、耐障害性が向上する

4. マルチAZ構成のメリットとデメリットは？
マルチAZでリソースを管理することで耐障害性が向上することがメリット
複数のリソースを使用することで、コストが向上することがデメリット

5. AWS Well-Architected Framework に定義されている６つの柱は？
セキュリティ、コスト最適化、信頼性、パフォーマンス効率
、運用上の優秀性、持続可能性


6. 所感、理解した点、気になった点
AWSのサービスが多数あり、ワークロードによってベストプラクティスに則ることで、セキュリティ、コスト、パフォーマンスなどを確保しながら、サービスを迅速に展開できることが学べたこと。

```

- AZ 間の通信には料金がかかる

  - 0.01USD/GB
  - WW で共通の料金

- Elastic Load Blanceing(ELB)
  - マルチリージョンに対応したマネージドサービス

# ラボ１

```shell
# リージョンを設定する
AZ=`curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone`
export AWS_DEFAULT_REGION=${AZ::-1}

# 最新の Linux AMI を取得する
AMI=$(aws ssm get-parameters --names /aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2 --query 'Parameters[0].[Value]' --output text)

echo $AMI
```

- サブネット取得

```shell
SUBNET=$(aws ec2 describe-subnets --filters 'Name=tag:Name,Values=LabPublicSubnet' --query Subnets[].SubnetId --output text)

echo $SUBNET
```

- セキュリティグループ取得

```shell
SG=$(aws ec2 describe-security-groups --filters Name=tag:Name,Values=LabInstanceSecurityGroup --query SecurityGroups[].GroupId --output text)

echo $SG
```

- スクリプトを取得する

```shell
cd ~
wget https://us-west-2-tcprod.s3.amazonaws.com/courses/ILT-TF-200-ARCHIT/v7.1.11.prod-3ad47223/lab-1-EC2/scripts/UserDataInstanceB.txt
```

- インスタンスを起動す r

```shell
INSTANCE=$(\
aws ec2 run-instances \
--image-id $AMI \
--subnet-id $SUBNET \
--security-group-ids $SG \
--user-data file://./UserDataInstanceB.txt \
--instance-type t3.micro \
--tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=InstanceB}]' \
--query 'Instances[*].InstanceId' \
--output text \
)
```

- インスタンスを表示す r

```shell
echo $INSTANCE
```

- インスタンス情報を取得する

```shell
aws ec2 describe-instances --instance-ids $INSTANCE
```

- インスタンス状態を取得する

```shell
aws ec2 describe-instances --instance-ids $INSTANCE --query 'Reservations[].Instances[].State.Name' --output text
```

- インスタンス DNS を取得する

```shell
aws ec2 describe-instances --instance-ids $INSTANCE --query Reservations[].Instances[].PublicDnsName --output text
```

# アカウントのセキュリティ

- 責任共有モデル

  - https://aws.amazon.com/jp/blogs/news/rethinksharedresponsibility/

- アンチパターン

  - ルートユーザで複数の使用者がログインして作業は行ってはいけない

- アクセスキー

  - プログラム用のアクセス情報

- IAM の機能

  - 認証を行う

    - アクセスしてきた人が誰なのかを確認する

  - 認可を行う
    - 認証したユーザのポリシー権限を確認する

- セキュリティプリンシパル

  - API を呼び出す主体
  - ルートユーザ
  - IAM ユーザ
  - AWS サービス
  - フェデレイテッドユーザ
    - 他の認証機関で認証されたユーザ

- アカウント

  - エイリアスを作成することが可能

- ポリシー例

  - どのリソースに対して
    - Resources
  - どのような操作を
    - Action
  - 許可する or 拒否する

    - Effect

  - アイデンティティポリシー
    - ユーザから見てどのリソースにアクセスできるのかを制御
    - サービスへのアクセス
    - 職務権限
  - リソースポリシー

    - リソースから見てどのユーザからアクセスできるのかを制御

  - 多層防御

  - ポリシー適用のルール
    - デフォルトは全て拒否
    - 部分的に Allow していく
    - Deny と Allow のポリシーが重なった部分は Deny の方が優先

- IAM ユーザグループ

  - グループ単位でポリシーを設定できる

- IAM ロール

  - CLI でのロール切り替え
    CLI は config よりも OS の環境情報のものを優先して利用する

    ```shell
    credentials=$(aws sts assume-role --role-session-name archdemo --role-arn arn:aws:iam::xxxxxxxxx:role/archDemoRole1115\
        --query "Credentials.[AccessKeyId, SecretAccessKey,SessionToken]" \
        --output text)

    export AWS_ACCESS_KEY_ID=$(echo $credentials | cut -f 1)
    export AWS_SECRET_ACCESS_KEY=$(echo $credentials | cut -f 2)
    export AWS_SESSION_TOKEN=$(echo $credentials | cut -f 3)
    ```

- AWS Organization

- モジュール２振り返り

```
1. ルートユーザを通常の運用で利用すべきではないのは？
ルートユーザは全てのアクセスが許可されており、複数人で運用したりするとパスワード流出によりアカウントが乗っ取られる可能性があるため

2. アプリケーションコードにIAMロールを使用した方が良いのは？
アプリケーションにアクセスキーを書くと、それを参照したユーザがアクセスキーを利用してリソースにアクセス可能になるため
IAMロールでは、一時的にアクセスが許可されるため、そのようなことが発生しない

3. AWSアカウントを管理していたユーザが退職した場合
ルートユーザのパスワードを変更して、退職したユーザがアクセスできないようにする。

4. AWS Organizationはどのように利用するサービス？
OUによってユニットを一括で管理する
また、アカウントをまとめて管理することでボリュームディスカントの恩恵を得ることが可能になる

5. IAMロールの仕組みによって柔軟で強固なセキュリティ管理の方法が可能になること
```

# モジュール４コンピューティング

- EC2 インスタンス

  - オンプレミス環境をクラウドへ移行する時に利用ケースが多い
  - 最近の Tech 系は、Lambda とかが多いかも
  - インスタンス->仮想サーバ

- Hypervisor

  - ナイトロ？？？

- demo

  ```shell
  #!/bin/bash -ex
  yum -y install httpd php
  systemctl enable httpd.service
  systemctl start httpd.service
  if [ ! -f /var/www/html/phpapp.zip ]; then
  cd /var/www/html
  wget https://training-nijot-org.s3.ap-northeast-1.amazonaws.com/arch/demo/mod3/phpapp.zip
  unzip phpapp.zip -d /var/www/html/
  fi
  ```

- インスタンス設定で新しい世代の方がコスト的には安くなる

- AWS Compute Optimizer

  - CloudWatch のメトリクスを解析して最適なインスタンスタイプを提示

- インスタンスメタデータ

  - インスタンスを説明するためのデータ
  - OS 内からインスタンスメタデータにアクセスすることが可能

- 料金オプション

  - リザーブドインスタンスは少しレガシーなプラン
    - 後から変更するようなことができない
    - 柔軟性が欠ける
  - Savings Plan の方が新しいプラン
    - インスタンスファミリーによって契約が可能
    - 柔軟性が高い

- EC2 スポットインスタンス

  - https://aws.amazon.com/jp/ec2/spot/testimonials/
  - https://aws.amazon.com/jp/blogs/news/how-dena-succesfully-applied-ec2-spot-on-production-and-reference-architecture-using-containers/
  - https://engineering.dena.com/blog/2019/08/cloud-qct-management/#%25E3%2582%25B9%25E3%2583%259D%25E3%2583%2583%25E3%2583%2588%25E3%2582%25A4%25E3%2583%25B3%25E3%2582%25B9%25E3%2582%25BF%25E3%2583%25B3%25E3%2582%25B9%25E3%2581%25B8%25E3%2581%25AE%25E6%258C%2591%25E6%2588%25A6

- ボリュームタイプ

  - SSD

    - IOPS
      - ランダムリードライトが良い

  - HDD
    - スループット
      - シーケンシャルリードライトが良い

- サーバーレス

  - 事例
    - https://www.businessinsider.jp/post-192845
    - https://speakerdeck.com/ikait/serverless-architecture-supports-nikkeis-paper-viewer
    - https://aws.amazon.com/jp/solutions/case-studies/asahi-shimbun/

- モジュール４振り返り

```
1. EC2インスタンスを起動するためのテンプレートは？
AMI（Amazon Machine Images）

2. EC2でビックデータを扱うための効率の良いEBSボリュームタイプは？
EBS HDD-Backedボリューム
スループットが良く、低コスト

3. インスタンスタイプを変更するための運用方法は？
インスタンスを停止し、インスタンスタイプを変更する

4. サーバーレスとはどういう考え方ですか？
アプリケーション開発に集中できるように、アプリケーション以下のレイヤーに関するメンテナンスはAWS側で行うサービス

5. 所感、理解した点、気になった点
オンプレミス環境をクラウドに移行する場合には、最初にEC2を利用することで、変更点を少なくして移行することが可能なこと。
また、サーバーレスに移行することで、運用リソースを開発リソースにシフトすることが可能になることが理解できた。

```

# モジュール３ネットワーク

- IPv4 サブネット計算機

  - https://www.vultr.com/ja/resources/subnet-calculator/?ip_address=172.31.0.0/16

- IPv6 のサブネットは /56 固定になっている

- Amazon VPC
  - リージョン単位で指定
  - Amazon Virtual Private Cloud
  - １アカウントでデフォルト５個
  - VPC を作成すると１つのメインルートテーブルが作成される
- サブネット
  - AZ 単位で指定する
  - パブリックサブネット
    - ルートテーブルにインターネットゲートウェイのエントリがあり
  - プライベートサブネット
    - ルートテーブルにインターネットゲートウェイのエントリがない
  - インターネットと VPC のルート設定
    1. IGW を VPC にアタッチする
    1. パブリックサブネット用ルートテーブルに igw を登録する
    1. リソースにパブリック IP アドレスを割り当てる
- インターネットゲートウェイ
  - 自動パブリック IP アドレスを有効化すると割り当てられる
    - ただし、インスタンスに割り当てられる IP は未定である
- ルートテーブル
- Elastic IP アドレス
  - 固定の IP アドレスを取得してリソースに割り当て可能
- NAT ゲートウェイ
- Elastic Network Interface

- VPC の多層防御

  - ネットワーク ACL
    - サブネットの境界でファイアウォールとして機能する
    - サブネットを守る
    - 規定では全てのインバウンド／アウトバウンドを許可
    - ステートレスで全てのトラフィックに明示的なルールが必要
  - セキュリティグループ
    - ENI を守る
    - AWS リソースのインバウンド／アウトバウンドを制御する仮想ファイアウォール
    - IP プロトコル、ポート、IP アドレスのトラフィックを許可する
    - ステートフルルールが適用される
    - セキュリティグループのチェーン
      - レイヤー構想でセキュリティグループを設定する
      - ウェブ層、アプリケーション層、データ層

- モジュール３振り返り

```
1. EC2インスタンスにインターネットからアクセスしたい場合、VPC /EC2の設定項目は？
サブネット作成
サブネットにIGWを配置
ルートテーブルを作成
サブネットにセキュリティグループを作成
リソースを作成して適切なサブネット／セキュリティグループを適用する

2. ENIとは？
インスタンスに設定する仮想イーサネットインターフェース

3. NATゲートウェイが必要なユースケースは？
プライベートサブネットに配置されたインスタンスのセキュリティアップデートをインターネットから取得する

4. ネットワークACLとセキュリティグループの違い？
セキュリティーグループはステートフル
ネットワークACLはステーツレス

5. 所感、理解した点、気になった点
VPCを利用したAWSのネットワーク作成を理解できた
```

# モジュール５ストレージ

- ブロックストレージ
  - 一箇所にデータが集まっている
  - 更新データの含まれるブロックのみを更新する
- オブジェクトストレージ

  - オブジェクト単位で分散して保持
  - 更新時には、オブジェクト全体を更新する

- Amazon Simple Storage Service(Amazon S3)

  - オブジェクト型ストレージ
  - 耐久性に優れている
  - マネージド型サービス
  - パブリックアクセスのブロック
    - 既定でオンになっているので、誤ってデータ公開するようなことはないようになっている
  - バージョニングが可能

  - オブジェクト単位でストレージクラスを変更することが可能
    - S3 - IA
    - Glacier
      - Flexible Retrieval
      - Instant Retrieval
      - Deep Archive
  - ライフサイクルポリシー

    - オブジェクトの保存期間に応じてストレージクラスを自動的に変更する

  - 保管時の暗号化

    - AWS で管理されるキー（SSE-S3）
    - AWS KMS で管理されるキー（SSE-KMS）
    - 自分で管理する(SSE-C)

  - Amazon S3 のコスト
    - コスト発生するもの
      - 1 ヶ月あたりの GB
      - PUT/COPY/POST/LIST/GET リクエスト数
      - 他のリージョンまたはインターネットへのデータ送信量
    - コスト発生しないもの
      - Amazon S3 へのデータ受信（IN）
      - 同じリージョンの AmazonEC2 または Cloud Front への送信（OUT）

- Amazon EFS

  - マウントターゲットは ENI

- Amazon FSx

  - Amazon FSx for Windows ファイルサーバ
  - Amazon FSx for Lustre

- モジュール振り返り

```
1. 医療系データ（ペタバイト）を何十年も保存し、且４８時間以内にアクセスするためのサービスは？
S3 Glacier Deep Archive

2. S3/Glacierの活用用途は？
業務で使用したデータを年ごとに保持する際に使用できるのでは

3. オンプレミスデータの移行に最適なサービスは？
AWS Snowball

4. 所感、理解した点、気になった点
信頼性を保持してデータ管理できるサービスS3について理解できた

```

- モジュール６データベース

- AWS が提供するデータベース

  - https://aws.amazon.com/jp/products/databases/
  - フルマネージドの目的に応じてデータベースを選択する

- リレーショナルデータベース
  - SQL による柔軟なクエリによるデータ取得
  - データ製合成が高い
  - スケーラビリティが低い
- 非リレーショナルデータベース

  - Read／Write が早い
  - スケーラビリティが高い

- Amazon RDS

  - Amazon Aurora 以外

    - マルチ AZ 配置
      - Amazon Aurora を除く
      - AZ 毎に DB インスタンスが配置される（プライマリ、スタンバイ）
        - プライマリとスタンバイはデータが同期される
      - アプリケーションからは、エンドポイントドメインにアクセスする
      - プライマリが死んだ場合、自動的にスタンバイにエンドポイントドメインが変わる
    - リードレプリカ
      - 読み取り専用のインスタンスによってリクエストを分散させることが可能
      - プライマリとリードレプリカは、非同期でレプリケーションされる
    - 暗号化
      - データベース全体が暗号化される

  - Amazon Aurora
    - MySQL,PostgreSQL と互換性あり
    - Amazon.com で使用している
    - スケーラビリティが高い
      - AZ を跨ってクラスターが生成される
      - リードインスタンスが自動的にプライマリに昇格する

- Amazon DynamoDB

  - フルマネージド型の NoSQL データベース
  - ユースケース
    - オンラインゲームのデータ
    - オンラインショッピングのショッピングカートとか（一時的なデータ）
  - バーティションキーによってデータ分散を決定
  - ソートキーによってクエリ機能を実現
  - スケーリング
    - プロビジョンドモード
      - キャパシティーユニット
        - １秒間に５回読み込み／書き込み
        - コストにかかる
        - オートスケーリングも可能
          - CloudWatch のメトリクスによって判断する
          - CloudWatch のメトリクス間隔は５分
    - オンデマンドモード
      - エッジの効いたスケーリングが可能
      - １リクエストにコストがかかる
  - 整合性オプション
    - 結果整合性
      - 一部のレプリカのデータを取得
      - コスト低
    - 強い整合性
      - 全てのレプリカのデータを取得
      - コスト高

- AWS DMS
  - データベース異種間移行が可能

# モジュール７モニタリングとスケーリング

- Amazon CloudWatch
  - メトリクスの収集
  - CloudWatch Agent によって自動収集する機能がある
  - 既定で取集するログ／メトリクスは AWS の管理内のみ
  - ログからメトリクスフィルタによってメトリクスに追加することが可能
- AWS CloudTrail
  - API のログを残す
- VPC フローログ
  - VPC 内のログを残す
  - 送信元／送信先／データ量／ステータス
- Amazon GuardDuty

  - API ログやフローログを解析するためのサービス

- CloudWatch アラーム

  - メトリクスに基づいてアラームを作成

- Elastic Load Blancing

  - ルール（リスナー）を複数設定可能
    - HTTP:80 とか
    - URL とか
  - Application Load Blancer
    - レイヤー７で動作する
  - Network Load Blancer
    - レイヤー４で動作する

- Auto Scaling

  - AWS Auto Scaling
    - 複数のサービスでスケーリングするサービスの総称
  - Amazon EC2 Auto Scaling
    - EC2 専用のスケーリングサービス

- モジュール７振り返り

```
1. CloudWatchとは？
EC2などのメトリクスを収集するサービス

2. CloudWatchで自動収集されるものは？
CPU使用率、メモリ使用量、ネットワーク送受信量

3. Auto Scalingのメリットは？
CloudWatchのメトリクスを利用して自動的にスケーリングできること
手動で設定する手間がなくなる

4. 所感、理解した点、気になった点
AWSの冗長性を確保するための考え方や方法を学ぶことができた
マニュアルを見ながらで理解できているが、細部にどの設定がどこに関連付けされているのかは、
練習を繰り返して学びたい

```

# モジュール８オートメーション

- 手動作業のメリット／デメリットは？

  - メリット
    - 項目の設定がわかりやすい
  - デメリット
    - 同じ作業を繰り返すのが面倒
    - 誤りが発生する場合がある

- CloudFormation

  - IaC
    - Infastructure as code
    - 宣言的コードによって最終的な状態をテンプレートを定義する
    - YAML はコメントが記載できるのでおすすめ
  - スタック
  - テンプレート
  - AWS ソリューション

  - 変更セット
    - 変更点のリストを AWS 側で提示する
  - 複数のテンプレートを使用する
    - 多層アーキテクチャー
      - フロントエンド
      - バックエンド
      - 共有
      - ベースネットワーク
      - アイデンティティ
  - 実装は？
    - テンプレートリファレンス
      - https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/template-reference.html
    - ソリューションライブラリ
      - 複数の AWS サービスを組み合わせてワークロードを解決する
      - https://aws.amazon.com/jp/solutions/
    - サンプルテンプレート
      - https://aws.amazon.com/jp/cloudformation/resources/templates/
    - AWS クラウド開発キット(CDK)
      - サポートされている言語でテンプレートを作成
      - CDK がポリシーを自動定義してくれる
      - コード作成中にエディタでミスを提示してくれる

- Systems Manager

  - 運用者が自動化するためのツールキット
  - インベントリ
    - インスタンスの状態（OS バージョン）を管理する
  - Run Command
    - 複数のインスタンスにコマンドを実行する
  - パッチマネージャ
    - インスタンスにパッチを適用する

- モジュール振り返り

```
1. CloudFormationのメリットは
リソースデプロイを自動化できる
差分を確認しながらデプロイすることができる

2. IaCを実践するにあたり管理は？
ベースは開発者が作成して構成管理ツールでテンプレートを管理する
運用者が別に存在するのであれば、テンプレートをレビューしてもらったりするのもあり

3. 所感、理解した点、気になった点
IaCが便利であることを理解した
デプロイが自動化でいるので、さらにアプリケーション開発に集中できるような気がした
VPCはリージョンで５つだと思いましたが、複数人でテンプレートを使用して作成すると上限を超えてしまうが、この場合上限を解除すれば良いのでしょうか？
```

- DevOps Engineering on AWS

  - https://aws.amazon.com/jp/training/classroom/devops-engineering-on-aws/

- CloudFormation テンプレートを自動生成する 3rd Party ツール

  - https://former2.com/
  - https://chrome.google.com/webstore/detail/console-recorder-for-aws/ganlhgooidfbijjidcpkeaohjnkeicba

- Service Quotas
  - サポートにリクエストが飛んで上限の制限を緩和する
  - VPC のネットワーク数など

# モジュール９コンテナ

- 「会議に出たくない」　デジタル庁、民間出身職員が反発

  - https://www.nikkei.com/article/DGXZQOUA119T20R10C22A4000000/

- コンテナサービス
  - Amazon Elastic Container Registory(ECR)
  - Amazon Elastic Container Service(ECS)
  - Amazon ESC オーケストレーション
    - サービス側でマルチ AZ 構成でクラスターを構築する
  - Amazon EKS
    - マネージドの Kubernetes サービス
  - AWS Fargete
    - マネージドのコンテナ環境

# モジュール１０ネットワーク２

- VPC エンドポイント

  - ゲートウェイエンドポイント(S3, DynamoDB)
    - レガシーなエンドポイント
  - インターフェースエンドポイント(S3, DynamoDB 以外の AWS API)
    - 新しいエンドポイント

- VPC ピアリング

  - VPC 間を接続する
  - リージョン内／外をサポート
  - １対１の通信

- Transit Gateway

  - VPC 同士をハブのように接続する
  - VPN の接続も可能

- AWS Site-to-Site VPN

  - IPSecVPN
  - メリットは手軽に開始することが可能
  - デメリットはインターネット回線なので通信がベストエフォートであること

- AWS Direct Connect

  - 専用線で接続する
  - Direct Connect ロケーション
    - 3rd Party Datacenter
    - https://aws.amazon.com/jp/directconnect/locations/

- Route 53
  - DNS サービス
  - パブリックホストゾーン
    - インターネットから名前解決が可能
  - プライベートホストゾーン
  - エッジロケーションで動作する
  - ルーティングポリシー
    - フェイルオーバー
    - 位置情報
  - 100%の動作保証

# モジュール１１サーバーレス

- サーバーレスアーキテクチャー

  - インフラ管理を必要としないアーキテクチャーで構築したサービス

- Amazon API Gateway

  - バックエンドへのリクエストの認証と認可を行う
  - サードパーティデベロッパによる API の使用量をスロットリング、測定、収益化する
  - エッジロケーションで動作する

- Amazon SQS
  - フルマネージド型のメッセージキューイングサービス
  - 標準キュー
    - 複数のデータセンターにキュー情報が分散配置される
    - 可視性タイムアウト
      - この間は他のコンシューマにはそのキューは見えない
      - コンシューマがメッセージ取得時に設定する
    - デッドレターキュー
      - 最大試行回数を超えたキュー退避する
  - FIFO キュー
    - 3000/秒
- Amazon Simple Notification Service(SNS)

  - パブリッシャー(送信者)
  - サブスクライバー(購読者)
  - Pub／Sub モデル

- SNS から複数の SQS キューへの通知

  - ファンアウト

- Amazon Kinesis

  - データストリームを処理する
  - データストリームとはリアルタイムに出力され続けるデータ
    - ログとか

- Step Functions
  - Lambda を利用したワークフローを実現する

# モジュール１２エッジサービス

- エッジとはユーザに近い拠点

  - エッジロケーション
  - AWS Outpost
    - AWS の仕組みをオンプレミスに展開する

- エッジロケーション

  - 世界中に４００箇所

- CloudFront

  - エッジロケーション内で動作する
  - CDN を提供するサービス
  - CloudFront の設定
    - オリジンを選択する
    - ディストリビューションを作成
    - オプション
      - WAF

- Amazon Global Accelerator

- DDoS 攻撃
  - WAF
    - Managed Rule
      - 専門家が考えたルール

# モジュール１３バックアップと復旧

- リージョンレベルで復旧を考える

  - ストレージ
  - AMI
  - データベースバックアップとレプリカ
  - テンプレートとスクリプト
    - リージョンによって使えるサービスなどもあるので確認しておく必要がある

# まとめ

```
1. 分かったこと、良かったこと
AWSのサービスを連携してソリューションを提供できるアーキテクチャーについて理解できた
AWSは今月くらいから触り始めてサービスが多く、どのように使用するかが全然分からなかったが、
今回の研修で全体感が理解できたことが良かった

2. 最後に一言
部分的に知っていたAWSのサービスですが、今回の研修でなんとなく繋がったような気がします。
今回の研修をベースにアーキテクチャーを構築できるようになれればと思います
三日間ありがとうございました
```
