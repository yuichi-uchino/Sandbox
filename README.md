# Sandbox
個人開発用サンドボックス環境

## 概要
Cloud Formationを使用して、AWS上にサンドボックス環境を構築するためのリポジトリです。

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
