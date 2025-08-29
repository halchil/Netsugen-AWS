# Netsugen-AWS


# VPC 

仕組み（シンプルな流れ）

プライベートサブネットにあるEC2が外部サイトにアクセス。

ルートテーブルで、0.0.0.0/0 のルートを NATゲートウェイ に向ける。

NATゲートウェイは、Elastic IP を使ってインターネットに通信。

応答はNATゲートウェイ経由でプライベートEC2に戻る。

## プライベートサブネット内のEC2に接続する際のベストプラクティス

方法1. Bastion Host（踏み台）を使う

パブリックサブネットに小さいEC2を立て、Elastic IPを付与

ローカルからその踏み台へSSH

踏み台からプライベートEC2へSSH（ssh -A でエージェント転送）


方法2. AWS Systems Manager (SSM) Session Managerを使う

パブリックIP不要、SSHポート開放不要

必要な設定：

SSMエージェントをEC2にインストール（Amazon Linux/UbuntuはデフォルトOK）

IAMロールに AmazonSSMManagedInstanceCore を付与

その後、AWS CLIから：

aws ssm start-session --target <instance-id>


もしくはAWSコンソールの「Session Manager」から直接シェル接続

➡ セキュリティ的には最強で、最近はこれが推奨


方法3. VPNやDirect Connect

オンプレや開発PCとAWS VPCをつなげて、
プライベートIPで直接アクセスできるようにする

Site-to-Site VPNやClient VPNを使う

➡ 本格的な構成向け
