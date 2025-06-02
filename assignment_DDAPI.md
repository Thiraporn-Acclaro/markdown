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

Your Datadog API key
===

A Kubernetes cluster has been provisioned for you as part of this lab environment. To begin, verify the cluster node and the version of Kubernetes it is running. 

1. In the terminal, run the following command:

```sh,run
kubectl get nodes
```

  You should see the following output.

  ![Output of kubectl get nodes](../assets/cluster_version_check.png)

A trial Datadog account has also been created for you. The credentials for this account are displayed in the terminal at the start of your session. You can retrieve them at any time by running:

```sh,run
creds
```

Use the credentials from this command to log in to [Datadog](https://app.datadoghq.com/).

Next, you will deploy the Datadog Agent in your Kubernetes cluster. The Agent requires an API key, which has already been set for you in the lab environment as the DD_API_KEY environment variable.

1. To confirm that the API key is available, run the following command:

```sh,run
echo $DD_API_KEY
```

Finish
===
When you're done, enter the following command in the terminal:

```sh,run
finish
```

Click the **Check** button in the lower right corner of the lab and wait for the results. Then select the **Next** button below the lab's frame to continue to the next section.
