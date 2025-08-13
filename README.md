# 概要

[aws-actions/aws-lambda-deploy](https://github.com/aws-actions/aws-lambda-deploy) Actionを使用してLambda関数をデプロイするためのサンプルです。

aws-actions/aws-lambda-deployはv1.0.1に基づきます。

補足等は以下記事を参照してください。  
https://dev.classmethod.jp/articles/aws-github-action-support-lambda-deploy/

## ファイル

このプロジェクトには、以下のディレクトリとファイルが含まれています：

```
.
├── hello_world/         # Lambda関数のソースコード
|   └── ...             # Lambda関数コード
└── templates/           # IAMロール作成用CloudFormationテンプレート
　   └── iam.yml         # GitHub Actions用とLambda実行用のIAMロール
```

## 必要な変数類

#### GitHub Actions環境での設定が必要な環境変数

| 環境変数名 | 説明 | 例 |
|-----------|------|-----|
| `AWS_ROLE_ARN` | GitHub Actions用IAMロールのARN(`iam.yml`で生成) | `arn:aws:iam::123456789012:role/github-actions-role` |
| `LAMBDA_FUNCTION_NAME` | Lambda関数名 | `sample-actions-deploy-function` |

#### CloudFormationテンプレートのパラメータ

`templates/iam.yml`をデプロイする際に指定するパラメータ：

| パラメータ名 | 説明 | デフォルト値 |
|-------------|------|-------------|
| `GitHubOrg` | GitHubユーザー名または組織名 | `cm-suzuki-junya` |
| `GithubRepoName` | 実行元リポジトリ名 | `sample-deploy-lambda-action` |
| `FunctionName` | 更新対象のLambda関数名 | `sample-actions-deploy-function` |

## セットアップ手順

`templates/iam.yml`を元に事前に必要なリソースを生成した後、GitHubリポジトリ側の環境変数を設定してください。

Lambda関数自体は初回のアクションに実行時に生成されます。IaC管理下には置かれないので消し忘れに注意してください。  
　=> 気になるのであれば別途CloudForimationやSAM等を利用して生成すれば良いです