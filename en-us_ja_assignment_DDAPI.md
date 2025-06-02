---
slug: datadog-api-key
type: challenge
title: Datadog API keys
notes:
- type: text
  contents: |-
    On this first track for the Progressive Delivery in Kubernetes course, you will get your environment setup for the rest of the course.

    ## Objectives

    - Get your newly created Datadog account set up
    - Deploy the Datadog Agent using the Datadog Helm chart
    - Get familiar with the e-commerce application you will be using throughout the course
    - Get familiar with the telemetry being sent to Datadog from your cluster and application

    Click the **Start** button below when your environment is ready.

    > **Note**: This lab will timeout after 10 minutes of inactivity.
tabs:
- title: Shell
  type: terminal
  hostname: progressive1-vm
- title: Help
  type: website
  url: https://datadoghq.dev/training-lab-support?sandboxId=${_SANDBOX_ID}
difficulty: basic
timelimit: 600
---

Datadog の API キー
===

このラボ環境には、Kubernetes クラスターがプロビジョニングされています。まず、クラスターのノードと、そのノードで稼働している Kubernetes のバージョンを確認しましょう。 

1. ターミナルで次のコマンドを実行します。

```sh,run
kubectl get nodes
```

  次の出力が表示されます。

  ![kubectl get nodes の出力](../assets/cluster_version_check.png)

Datadog トライアルアカウントも作成されています。このアカウントの認証情報は、セッション開始時にターミナルに表示されます。次のコマンドを実行することで、いつでも確認できます。

```sh,run
creds
```

このコマンドで表示される認証情報を使って、[Datadog](https://app.datadoghq.com/) にログインします。

次に、Kubernetes クラスターに Datadog Agent をデプロイします。Agent には API キーが必要ですが、このラボ環境ではすでに DD_API_KEY 環境変数で設定されています。

1. API キーが利用可能であることを確認するには、次のコマンドを実行します。

```sh,run
echo $DD_API_KEY
```

完了
===
完了したら、ターミナルで次のコマンドを入力してください。

```sh,run
finish
```

ラボ画面の右下にある **\[Check (チェック)\]** ボタンをクリックし、結果が表示されるまで待ちます。その後、ラボの表示領域の下にある **\[Next (次へ)\]** ボタンを選択して、次のセクションに進んでください。
