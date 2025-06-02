---
slug: deploy-datadog
type: challenge
title: Deploy Datadog
teaser: Deploy Datadog in your cluster with the Helm Chart
notes:
- type: text
  contents: |
    You are going to deploy the Datadog Agent using its Helm Chart

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

Datadog Helm チャートのデプロイ
===

まず、API キーを指定して Datadog の Helm チャートをデプロイします。

```sh,run
helm install datadog \
  --set datadog.apiKey=$DD_API_KEY datadog/datadog \
  -f /root/manifest-files/datadog/datadog-helm-values.yaml \
  --version=2.16.6
```

次のコマンドを実行して、デプロイされたワークロードを確認します。 

```sh,run
kubectl get deployments
```

次のような出力が表示されます。

```nocopy
NAME                         READY   UP-TO-DATE   AVAILABLE   AGE
datadog-cluster-agent        1/1     1            1           5s
datadog-kube-state-metrics   1/1     1            1           1m
```

次のコマンドを実行して、Node Agent の DaemonSet を確認します。 

```sh,run
kubectl get daemonset
```

次のような出力が表示されます。

```nocopy
NAME      DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR            AGE
datadog   1         1         1       1            1           kubernetes.io/os=linux   22h
```

Datadog の Helm チャートは、デフォルトで [Datadog Node Agent](https://docs.datadoghq.com/agent/kubernetes/?tab=helm)、[Datadog Cluster Agent](https://docs.datadoghq.com/agent/cluster_agent/)、[Kube State Metrics](https://github.com/kubernetes/kube-state-metrics) という 3 つのワークロードをデプロイします。Kube State Metrics は、Kubernetes API を監視し、オブジェクトの状態に関するメトリクスを生成するサービスです。Datadog は、これらのメトリクスの一部を使用して、Kubernetes のデフォルトダッシュボードを表示します。

次のコマンドを実行して、Datadog Agent が稼働するまで待ちます。

```sh,run
/root/wait-datadog.sh
```

`datadog` Pod が稼働したら、次のコマンドを実行してそのステータスを確認します。

```sh,run
kubectl exec -ti ds/datadog -- agent status
```

出力内容を確認しましょう。Datadog Agent はどのチェックを実行していますか?まだ `kubelet` チェックが実行されていない場合は、上記のコマンドを再実行し、`kubelet` チェックが動作するのを確認してから次のステップに進んでください。

```nocopy
kubelet (7.1.0)
---------------
  Instance ID: kubelet:5bbc63f3938c02f4 [OK]
  Configuration Source: file:/etc/datadog-agent/conf.d/kubelet.d/conf.yaml.default
  Total Runs: 19
  Metric Samples: Last Run: 3,733, Total: 70,862
  Events: Last Run: 0, Total: 0
  Service Checks: Last Run: 4, Total: 76
  Average Execution Time : 1.842s
  Last Execution Date : 2022-01-25 10:02:40 UTC (1643104960000)
  Last Successful Execution Date : 2022-01-25 10:02:40 UTC (1643104960000)
```

> [!NOTE]
> 出力「`Error: unable to read authentication token file: open /etc/datadog-agent/auth_token`」が表示される場合、これは一時的なエラーであるため、コマンドを再実行してください。

Datadog Agent はそのまま実行状態にしておいてください。メトリクスやログは引き続き Datadog に送信されます。

完了
===

ラボ画面の右下にある **\[Check (チェック)\]** ボタンをクリックし、結果が表示されるまで待ちます。
