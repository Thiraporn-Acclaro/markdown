---
slug: browse-the-app
type: challenge
title: Browse the e-commerce application
teaser: Get familiar with the e-commerce application
notes:
- type: text
  contents: |
    You will get familiar with the e-commerce application you will be using throughout the course.

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

The e-commerce application
===

The e-commerce application is already provisioned for you in the `ns1` namespace. You can check the different deployments that are part of the application by running the following command:

```sh,run
kubectl get deployment -n ns1 --selector=app=ecommerce && kubectl get deployment -n database
```

You should get output similar to this:

```nocopy
NAME             READY   UP-TO-DATE   AVAILABLE   AGE
advertisements   1/1     1            1           15m
discounts        1/1     1            1           15m
frontend         1/1     1            1           15m
NAME   READY   UP-TO-DATE   AVAILABLE   AGE
db     1/1     1            1           15m
```

The e-commerce application consists of a big monolith application called `frontend`, a microservice that serves advertisements, a microservice that serves discounts coupons, and a postgres database.

Check that all the pods are running correctly by running the following command:

```sh,run
kubectl get pods -n ns1 --selector=app=ecommerce && kubectl get pods -n database
```

At this point you can visit the e-commerce application by clicking on the **Ecommerce App** tab in the terminal. Browse around to familiarize yourself with the application. Can you tell what areas of web page are served by the `advertisements` and `discounts` microservices?

To make it clearer when you are doing the progressive delivery, version `1.0` of the `advertisements` service is alway displays an ad banner that clearly says `Version 1.0`. 
This will help you identify that version easily.

![Screenshot of Ecommerce app](../assets/app.png)

> [!NOTE]
> If you get an error like the one shown below, refresh the page. It happens
  when the database is still initializing:

  ![Screenshot of DB error](../assets/db_error.png)

Finish
===
If you've viewed the application, enter the following command in the terminal:

```sh,run
finish
```

Click the **Check** button in the lower right corner of the lab and wait for the results.
