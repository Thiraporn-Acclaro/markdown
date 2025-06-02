---
slug: browse-datadog
type: challenge
title: Browse Datadog
teaser: Browse Datadog for telemetry from your cluster and application
notes:
- type: text
  contents: |
    Browse Datadog to see what telemetry data you are getting.

    Click the **Start** button below when your environment is ready.

    > **Note**: This lab will timeout after 10 minutes of inactivity.
tabs:
- title: Shell
  type: terminal
  hostname: progressive1-vm
- title: Ecommerce App
  type: service
  hostname: progressive1-vm
  path: /
  port: 30001
  new_window: true
- title: Help
  type: website
  url: https://datadoghq.dev/training-lab-support?sandboxId=${_SANDBOX_ID}
difficulty: basic
timelimit: 600
---

Datadog インターフェイス
===

アプリケーションの起動と Datadog のデプロイが完了すると、Datadog アカウントでデータが表示されるようになります。 

## ライブコンテナ

ラボ用に作成したアカウントを使って、[Datadog アプリ](https://app.datadoghq.com)にログインしてください。`creds` コマンドを実行すると、任意のラボ用ターミナルでこのアカウントの認証情報を表示できます。

```sh,run
creds
```

**[\[Infrastructure (インフラストラクチャ)\] > \[Containers (コンテナ)\]](https://app.datadoghq.com/containers)** に移動し、稼働中のコンテナを確認します。ページにデータが反映されるまでに、数分かかることがあります。Datadog にデータが取得され始めると、下のスクリーンショットのような画面が表示されます。

![\[Live Containers (ライブコンテナ)\] ページのスクリーンショット](../assets/live_containers.png)

**\[Containers (コンテナ)\]** ページでは、Kubernetes クラスター内で稼働しているコンテナに関するすべての情報を 1 か所で確認できます。クラスター内のすべての Deployment を名前空間ごとにグループ化して表示するには、次の操作を行ってください。

1. グローバルナビゲーションで、**[\[Infrastructure (インフラストラクチャ)\] > \[Kubernetes Overview (Kubernetes の概要)\]](https://app.datadoghq.com/kubernetes)**をクリックします。

1. \[**DEPLOYMENTS (Deployment)**\] リソースをクリックします。

1. ページ上部の \[**Group by (グループ化)**\] フィールドに、次のコマンドを入力します。

   ```sh,run
   kube_namespace
   ```

   ![kube_namespace タグで Deployment をグループ化する](../assets/group_by_kube_namespace.png)

1. ページ上部で **[\[Map (マップ)\]](https://app.datadoghq.com/orchestration/map/deployment?groups=kube_namespace&metric=deployment.uptime&paused=false)** タブをクリックします。

![\[Map (マップ)\] タブのスクリーンショット](../assets/cluster_map.png)

**\[Kubernetes\]** ビューをさらに確認してみましょう。他にどのような情報が見つかりますか?

## Software Catalog

アプリケーションには分散トレーシングがすでにインスツルメントされているため、アプリケーションへのリクエストがあるたびに、トレースとスパンのセットが生成されます。データを確認できるように、アプリケーションにはトラフィックが発生するようになっています。

1. **[\[Service Management\] > \[Software Catalog\]](https://app.datadoghq.com/services?env=progressive&hostGroup=) に移動します。** 
   Software Catalog が開き、\[**Ownership (オーナーシップ)**\] タブが表示されます。
1. **\[Reliability (信頼性)\]** タブをクリックすると、分散トレーシングから特定された
   Storedog サービスのリストが表示されます。

Datadog Software Catalog は、組織内のすべてのサービスに関する重要情報をまとめて確認できる場所です。大規模な運用でもサービスをエンドツーエンドで管理できます。また、リアルタイムのパフォーマンスインサイトを取得し、信頼性やセキュリティのリスクを検出して対処し、アプリケーションの依存関係を一か所で管理できます。Slack などのチームコミュニケーションツール、GitHub などのソース管理ツール、Datadog のダッシュボード、そして各サービスのテレメトリーデータを受信して監視する Datadog のビューにアクセスできます。

> [!NOTE]
> Software Catalog でサービスを表示するためにインスツルメントを行う必要はありません。メタデータは、内容を記述した YAML ファイルをアップロードすることで追加できます。詳しくは、[Software Catalog](https://docs.datadoghq.com/software_catalog/) のドキュメンテーションをご覧ください。

![\[Service List (サービスリスト)\] ページのスクリーンショット](../assets/service_list.png)

どのようなサービスが表示されていますか?それぞれのサービスについて、どのような情報が得られますか?

1. **\[Map (マップ)\]** をクリックすると、同じ情報を視覚的に確認できます。環境セレクターが `env:progressive` 
に設定されていることを確認してください。

Service Map (サービスマップ) を使うと、アプリケーション内でどのサービスが相互に通信しているかを把握できます。この可視化には数分かかることがあるため、表示が空白の場合は、しばらく時間をおいてからコースの後半で再度確認してください。マップが生成されると、下のグラフのように表示されます。

![\[Service Map (サービスマップ)\] ページのスクリーンショット](../assets/service_map.png)

異なるサービスの上にカーソルを合わせると、トラフィックやレイテンシが可視化されます。

完了
===

上記の Datadog セクションを確認したら、ターミナルで次のコマンドを入力してください。

```sh,run
finish
```

ラボ画面の右下にある** \[Check (チェック)\] **ボタンをクリックし、結果が表示されるまで待ちます。その後、ラボの表示領域の下にある **\[Next (次へ)\]** ボタンを選択して、次のセクションに進んでください。
