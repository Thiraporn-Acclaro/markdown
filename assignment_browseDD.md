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

Datadog interface
===

Your application up and running and you have deployed Datadog to it. You should start seeing data in your Datadog account. 

## Live Containers

Login to the [Datadog App](https://app.datadoghq.com) now using the account created for you for the labs. You can display the credentials for this account in any lab terminal by executing the command `creds`:

```sh,run
creds
```

Navigate to **[Infrastrucutre > Containers](https://app.datadoghq.com/containers)** and browse the running containers. Take into account that it may take some minutes for the data to populate that page. Once you start getting data into Datadog you should see something similar to the screenshot below:

![Screenshot of the Live Containers page](../assets/live_containers.png)

In the **Containers** page you can have all the information about the containers running in your Kubernetes cluster in a single place. To see a visualization of all Deployments in your cluster grouped by namespace, do the following:

1. In the global navigation, click **[Infrastructure > Kubernetes Overview](https://app.datadoghq.com/kubernetes)**.

1. Click on the **DEPLOYMENTS** resource.

1. At the top of the page, in the **Group by** field, enter the following:

   ```sh,run
   kube_namespace
   ```

   ![Group deployments by kube_namespace tag](../assets/group_by_kube_namespace.png)

1. At the top of the page, click the **[Map](https://app.datadoghq.com/orchestration/map/deployment?groups=kube_namespace&metric=deployment.uptime&paused=false)** tab.

![Screenshot of the Map tab](../assets/cluster_map.png)

Continue to browse around the **Kubernetes** view. What other information are you finding?

## Software Catalog

Your application is already instrumented for distributed tracing, so any request made to the application will generate a trace and a set of spans. Traffic is being generated for the application to ensure there is data to explore.

1. Navigate to **[Service Management > Software Catalog](https://app.datadoghq.com/services?env=progressive&hostGroup=)**. 
   This will open the Software Catalog to the **Ownership** tab.
1. Click the **Reliability** tab to see a list of the Storedog services identified
   from distributed tracing.

Datadog Software Catalog is a centralized place to access important information about all services in your organization. Achieve end-to-end service ownership at scale, get real-time performance insights, detect and address reliability and security risks, and manage application dependencies all in one place. Access team communications tools such as Slack, source control such as GitHub, Datadog dashboards, and Datadog views that receive and monitor telemetry data for each service.

> [!NOTE]
> You do not need to instrument your service for it to appear in Software Catalog. Its metadata can be added by uploading a YAML file with this metadata. Read more about this in the documentation for [Software Catalog](https://docs.datadoghq.com/software_catalog/).

![Screenshot of the Service List page](../assets/service_list.png)

What services do you see? What type of information are you getting for each of those?

1. Click **Map** to get the same information in a visual way. Make sure that 
the environment selector is set to `env:progressive`.

The Service Map helps with understanding what services talk to each other in the application. This visualization may take several minutes to populate, so if this is blank for you, come back later in the course to view it. Once it populates it will look similar to the graph below:

![Screenshot of the Service Map page](../assets/service_map.png)

Hover over the different services to visualize traffic and latency.

Finish
===

If you've browsed the Datadog sections mentioned, enter the following command in the terminal:

```sh,run
finish
```

Click the **Check** button in the lower right corner of the lab and wait for the results. Then select the **Next** button below the lab's frame to continue to the next section.
