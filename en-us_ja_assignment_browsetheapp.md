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

E コマースアプリケーション
===

この E コマースアプリケーションは、すでに `ns1` 名前空間にプロビジョニングされています。アプリケーションを構成する各種 Deployment を確認するには、次のコマンドを実行します。

```sh,run
kubectl get deployment -n ns1 --selector=app=ecommerce && kubectl get deployment -n database
```

次のような出力が表示されます。

```nocopy
NAME             READY   UP-TO-DATE   AVAILABLE   AGE
advertisements   1/1     1            1           15m
discounts        1/1     1            1           15m
frontend         1/1     1            1           15m
NAME   READY   UP-TO-DATE   AVAILABLE   AGE
db     1/1     1            1           15m
```

この E コマースアプリケーションは、`frontend` という大規模なモノリスアプリケーション、広告を提供するマイクロサービス、割引クーポンを提供するマイクロサービス、そして postgres データベースで構成されています。

すべての Pod が正しく稼働していることを確認するには、次のコマンドを実行します。

```sh,run
kubectl get pods -n ns1 --selector=app=ecommerce && kubectl get pods -n database
```

この時点で、ターミナル内の **\[Ecommerce App (E コマースアプリ)\]** タブをクリックすると、E コマースアプリケーションにアクセスできます。アプリケーションの各部分を見て、その構成に慣れておきましょう。Web ページのどの部分が、`advertisements` マイクロサービスや `discounts` マイクロサービスによって提供されているか分かりますか?

プログレッシブデリバリーを行う際にバージョンを明確にするため、`advertisements` サービスのバージョン `1.0` では、「`Version 1.0`」と明記された広告バナーが常に表示されます。 
これにより、バージョンを簡単に識別できます。

![E コマースアプリのスクリーンショット](../assets/app.png)

> [!NOTE]
> 以下のようなエラーが表示された場合は、ページを再読み込みしてください。このエラーは、
  データベースの初期化がまだ完了していない場合に発生することがあります。

  ![DB エラーのスクリーンショット](../assets/db_error.png)

完了
===
アプリケーションの確認が終わったら、ターミナルで次のコマンドを入力してください。

```sh,run
finish
```

ラボ画面の右下にある **\[Check (チェック)\]** ボタンをクリックし、結果が表示されるまで待ちます。
