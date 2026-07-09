# Sandbox
個人開発用サンドボックス環境

## 概要
Cloud Formationを使用して、AWS上にサンドボックス環境を構築するためのリポジトリです。
ALB + ASG + EC2 + Docker + ECR Pull + NATなしVPC Endpoint構成でリソースを作成します。

## AWS環境
アカウントID: 970817257744

## 課金対象のリソースを管理しているスタック
- alb-stack
- endpoint-stack
- app-stack

## よく使うコマンド

### ログインと確認
```bash
aws login
aws sts get-caller-identity
aws configure list
```

### テンプレート構文チェック

```bash
aws cloudformation validate-template \
  --template-body file://{yamlファイル名}
```

### 変更内容の確認用 Change Set 作成
```bash
aws cloudformation deploy \
  --stack-name {スタック名} \
  --template-file {yamlファイル名} \
  --parameter-overrides Environment={環境} \
  --no-execute-changeset \
  --region ap-northeast-1
```

### IAM ROLEの変更がある場合は、追加のプロパティが必要
```bash
--capabilities CAPABILITY_IAM
````

### 名前付きIAMリソースを作る場合は、追加のプロパティが必要
```bash
--capabilities CAPABILITY_NAMED_IAM
```

### 変更内容の確認
```bash
aws cloudformation describe-change-set \
  --change-set-name {ChangeSet名またはARN} \
  --region ap-northeast-1 \
  > "changeset.json"
```

### 問題なければ実行
```bash
aws cloudformation deploy \
  --stack-name {スタック名} \
  --template-file {yamlファイル名} \
  --parameter-overrides Environment={環境} \
  --region ap-northeast-1
```

### IAM ROLEの変更がある場合は、追加のプロパティが必要
```bash
--capabilities CAPABILITY_IAM
````

### スタック削除
```bash
aws cloudformation delete-stack \
  --stack-name {スタック名} \
  --region ap-northeast-1
```
