---
layout: classic-docs
title: "Orbs、ジョブ、ステップ、ワークフロー"
short-title: "Orbs、ジョブ、ステップ、ワークフロー"
description: "ジョブとステップの説明"
categories:
  - migration
order: 2
---

ここでは、ジョブ、ステップ、ワークフローに加え、Orbs に使用される新しい [`.circleci/config.yml`]({{ site.baseurl }}/ja/2.0/configuration-reference/) キーの概要について説明します。

- 目次
{:toc}

## Orbs の概要

Orbs は、名前に基づいてインポートするか、インラインで設定するコンフィグのパッケージです。コンフィグを簡略化し、プロジェクト内またはプロジェクト間でコンフィグを共有および再利用するために使用されます。 コンフィグで Orbs を使用する方法と Orb 設計の概要については、「[Orbs を使う]({{ site.baseurl }}/ja/2.0/using-orbs/)」を参照してください。 Visit the [Orbs Registry](https://circleci.com/orbs/registry/) to search for orbs to help simplify your config.

## ジョブの概要

ジョブはステップの集まりです。 ジョブ内のステップはすべて 1単位として実行され、その際にプランから CircleCI コンテナが 1つ消費されます。

ジョブとステップはきめ細かく制御できます。ワークフローのフレームワークが提供され、各フェーズでのステータスを確認できるため、高頻度のフィードバックが可能になります。 下図はジョブ間のデータフローを表したものです。 ワークスペースは、同じワークフロー内のジョブ間でデータを維持します。 キャッシュは、異なるワークフロービルドにある同じジョブ間でデータを維持します。 アーティファクトは、ワークフローの終了後にデータを維持します。

![ヘッダー]({{ site.baseurl }}/assets/img/docs/Diagram-v3--Default.png)

2.0 のジョブは、最近使用された `machine` Executor の実行を再利用できる `machine` Executor、テストや必要なサービス (データベースなど) を実行するように Docker コンテナを構成できる `docker` Executor、または `macos` Executor を使用して実行できます。

`docker` Executor を使用する場合、起動するコンテナは、`docker:` キーの下にリストされるコンテナイメージで指定されます。 `docker` Executor と共に任意のパブリック Docker イメージも使用できます。

`docker` Executor と `machine` Executor の用途と違いについては、[コンテナイメージの指定に関するドキュメント]({{ site.baseurl }}/ja/2.0/executor-types/)を参照してください。

## ステップの概要

ステップは、ジョブ中に実行される実行可能なコマンドの集まりです。コードをチェックアウトするには `checkout:` キーを指定する必要があります。また、`run:` キーを使用すると、複数行にわたる任意のシェルコマンドスクリプトを追加できます。 `run:` キーに加えて、`save_cache:`、`restore_cache:`、`deploy:`、`store_artifacts:`、`store_test_results:`、`add_ssh_keys` などのキーがステップの下にネストされます。

## インポートした Orb を使用した設定例

```yaml
version: 2.1

orbs:
  aws-s3: circleci/aws-s3@1.0.0 #imports the s3 orb in the circleci namespace

workflows:
  build-test-deploy:
    jobs:

      - deploy2s3: # a sample job that would be defined above.
          steps:
            - aws-s3/sync: #invokes the sync command declared in the s3 orb
                from: .
                to: "s3://mybucket_uri"
                overwrite: true
```

## 並列ジョブの設定例

2.0 `.circleci/config.yml` ファイルの例を以下に示します。

{% raw %}
version: 2
    jobs:
      build:
        docker:
    
          - image: circleci/<language>:<version TAG>
        steps:
          - checkout
          - run: <command>
      test:
        docker:
          - image: circleci/<language>:<version TAG>
        steps:
          - checkout
          - run: <command>
    workflows:
      version: 2
      build_and_test:
        jobs:
          - build
          - test
    

{% endraw %} 上記は並列ジョブワークフローの例です。処理時間を短縮するために、`build` ジョブと `test` ジョブを並列で実行しています。 並列実行、順次実行、および手動承認のワークフローによってジョブをオーケストレーションする詳しい方法については「[ジョブの実行を Workflow で制御する]({{ site.baseurl }}/ja/2.0/workflows)」を参照してください。

## 関連項目

- [設定リファレンス：jobs キー]({{ site.baseurl }}/ja/2.0/configuration-reference/#jobs)
- [設定リファレンス：steps キー]({{ site.baseurl }}/ja/2.0/configuration-reference/#steps)