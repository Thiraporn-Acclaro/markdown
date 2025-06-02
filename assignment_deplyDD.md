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

Deploy the Datadog Helm Chart
===

First, deploy the Datadog Helm chart, passing your API key:

```sh,run
helm install datadog \
  --set datadog.apiKey=$DD_API_KEY datadog/datadog \
  -f /root/manifest-files/datadog/datadog-helm-values.yaml \
  --version=2.16.6
```

Check the workloads that have been deployed. Run the following command:

```sh,run
kubectl get deployments
```

You should get output similar to the following

```nocopy
NAME                         READY   UP-TO-DATE   AVAILABLE   AGE
datadog-cluster-agent        1/1     1            1           5s
datadog-kube-state-metrics   1/1     1            1           1m
```

Now check the Node Agent Daemonset. Run the following command:

```sh,run
kubectl get daemonset
```

You should see output similar to the following:

```nocopy
NAME      DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR            AGE
datadog   1         1         1       1            1           kubernetes.io/os=linux   22h
```

The Datadog Helm chart, by default, deploys three workloads: the [Datadog Node Agent](https://docs.datadoghq.com/agent/kubernetes/?tab=helm), the [Datadog Cluster Agent](https://docs.datadoghq.com/agent/cluster_agent/), and [Kube State Metrics](https://github.com/kubernetes/kube-state-metrics) by default. Kube State Metrics is a service that listens to the Kubernetes API and generates metrics about the state of the objects. Datadog uses some of these metrics to populate its Kubernetes default dashboard.

Wait until the Datadog Agent is running by executing this command:

```sh,run
/root/wait-datadog.sh
```

Once the `datadog` pod is running, check its status by running the following command:

```sh,run
kubectl exec -ti ds/datadog -- agent status
```

Browse the output. What checks is the Datadog Agent running? If the `kubelet` check is not yet running, rerun the command above until you see the `kubelet` check running before moving to the next step.

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
> If you get the following output: `Error: unable to read authentication token file: open /etc/datadog-agent/auth_token`, just rerun the command, as this is a transient error.

Leave the Datadog Agent running. It will send metrics and logs to Datadog.

Finish
===

Click the **Check** button in the lower right corner of the lab and wait for the results.
