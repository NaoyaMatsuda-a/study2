# aws-autoscaling-alb-demo
Auto Scaling Group + Application Load Balancer による Webサーバーのスケーラブル構成（初中級向け）

---

## 📝 プロジェクト概要

本プロジェクトでは、AWSのAuto Scaling Group（ASG）とApplication Load Balancer（ALB）を活用して、高可用性と自動スケーリングを備えたWebサーバー環境を構築しました。  
起動テンプレートを用いてApacheが自動起動するAmazon Linux 2インスタンスを複数AZに展開し、ALB配下でトラフィック分散を実現しています。

---

## ☁️ 使用したAWSサービス

- VPC（CIDR: 10.1.0.0/16）
- パブリックサブネット（2AZ構成）
- インターネットゲートウェイ（IGW）
- ルートテーブル
- セキュリティグループ（ALB用・EC2用）
- EC2 + 起動テンプレート（Apacheインストール済み）
- ALB（Application Load Balancer）
- ターゲットグループ（HTTP/80）
- Auto Scaling Group（最小1 / 最大2）

---

## 🖼️ 構成図

※構成図画像をここに貼ってください  
例: `![構成図](構成図URL)`

---

## ⚙️ 作業手順概要

1. VPC作成（10.1.0.0/16）
2. パブリックサブネット作成（2AZ、10.1.1.0/24, 10.1.2.0/24）
3. IGW作成・VPCへアタッチ
4. ルートテーブル作成・2つのサブネットと関連付け
5. セキュリティグループ作成（ALB: 80番 / EC2: 22,80番）
6. ALB作成 + ターゲットグループ作成（HTTPヘルスチェック設定）
7. 起動テンプレート作成（Apache自動インストールスクリプト含む）
8. Auto Scaling Group作成（ALBに連携、AZ分散）
9. 動作確認（ALBドメインにアクセスしApacheページ表示）

---

## 💻 接続・確認画面

### ✅ ssh接続確認
※スクショを貼ってください（PuTTY or ターミナル）

### ✅ ヘルスチェック確認
※ALBターゲットの正常ステータスのスクショ

### ✅ Webブラウザ確認
`http://{ALBのDNS名}` にアクセスし、Apacheページ表示

---

## 📚 学び・気づき

- ApacheインストールをUserDataで自動化する重要性
- セキュリティグループが ALB → EC2 で許可されていないと通信できない
- ヘルスチェックのステータスによってAuto Scalingがインスタンスを自動置換する仕組みの理解
- 起動テンプレートを使うと設定ミス時の管理がしやすい

---

## 🚀 今後のチャレンジ

- CloudWatchアラームによるスケーリングポリシー追加
- Route53連携による独自ドメイン運用
- TerraformによるIaC化（再現性のある構築）

---

## 🗂️ 補足：使用AMI
- Amazon Linux 2（ID: ami-xxxxxxxxxxxxxxxxx）  
※起動テンプレートに明記しています。

---

## 🔗 GitHubリンク
リポジトリURL: `https://github.com/yourname/aws-autoscaling-alb-demo`
