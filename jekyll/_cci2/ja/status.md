---
layout: classic-docs
title: "ステータス"
short-title: "ステータス"
description: "ステータス ダッシュボード"
categories:
  - getting-started
order: 1
---

<hr />

| バッジ                                                                                     | デバッグ                                                                                          |
| --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| インテグレーションを利用して、[他の Web ページにステータス バッジを追加]({{ site.baseurl }}/2.0/status-badges/)ことができます。 | ビルドのトラブルシューティングが必要なときは、[SSH を使用して、失敗したビルドをデバッグ]({{ site.baseurl }}/2.0/ssh-access-jobs/)できます。 |

<hr />

| キューイング                                                                                                                                                                               |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ジョブの待機時間が発生している場合は、[Performance プランまたは Custom プラン](https://circleci.com/ja/pricing/)への切り替えによって解消できる可能性があります。 詳細については、[クレジットの使用に関するドキュメント]({{ site.baseurl }}/2.0/credits/)を参照してください。 |

<hr />

![ワークフローの図]({{ site.baseurl }}/assets/img/docs/job_status.png)

CircleCI の統合ダッシュボードでは、最後に完了したジョブ実行について以下のステータスが表示されます。

- SUCCESS: すべてのジョブが成功
- FAILED: 1 つ以上のジョブが失敗

[ワークフロー]({{ site.baseurl}}/2.0/workflows/#概要)を使用している場合は、上記に加えて[ワークフロー固有のステータス]({{ site.baseurl}}/2.0/workflows/#ステータス)が表示されます。