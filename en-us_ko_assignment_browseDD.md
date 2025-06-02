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

Datadog 인터페이스
===

애플리케이션이 정상적으로 실행 중이며, 애플리케이션에 Datadog을 배포했습니다. 이제 Datadog 계정에 데이터가 표시됩니다. 

## 라이브 컨테이너

이제 실습용으로 생성된 계정을 사용해 [Datadog 앱](https://app.datadoghq.com)에 로그인하세요. 실습 터미널에서 `creds` 명령을 실행하여 이 계정의 자격 증명을 표시할 수 있습니다.

```sh,run
creds
```

**[Infrastrucutre(인프라스트럭처) > Containers(컨테이너)](https://app.datadoghq.com/containers)** 로 이동하여 실행 중인 컨테이너를 살펴보세요. 해당 페이지에 데이터가 채워지는 데는 몇 분 정도 걸릴 수 있습니다. Datadog에 데이터가 수집되기 시작하면 아래 스크린샷과 유사한 화면이 표시됩니다.

![라이브 컨테이너 페이지 스크린샷](../assets/live_containers.png)

**Containers(컨테이너)** 페이지에서는 Kubernetes 클러스터에서 실행 중인 컨테이너에 대한 모든 정보를 한곳에서 확인할 수 있습니다. 클러스터 내 모든 배포 항목을 네임스페이스별로 그룹화하여 표시하려면 다음과 같이 하세요.

1. 글로벌 탐색 메뉴에서 **[Infrastructure(인프라스트럭처) > Kubernetes Overview(Kubernetes 개요)](https://app.datadoghq.com/kubernetes)** 를 클릭합니다.

1. **DEPLOYMENTS(배포)** 리소스를 클릭합니다.

1. 페이지 상단의 **Group by**(그룹화 기준) 필드에 다음을 입력합니다.

   ```sh,run
   kube_namespace
   ```

   ![kube_namespace 태그를 기준으로 배포 그룹화](../assets/group_by_kube_namespace.png)

1. 페이지 상단의 **[Map(맵)](https://app.datadoghq.com/orchestration/map/deployment?groups=kube_namespace&metric=deployment.uptime&paused=false)** 탭을 클릭합니다.

![Map(맵) 탭 스크린샷](../assets/cluster_map.png)

**Kubernetes** 뷰를 계속 탐색해 보세요. 다른 어떤 정보들이 보이나요?

## Software Catalog

애플리케이션에 이미 분산 트레이싱을 위한 인스트루먼테이션이 구현되어 있으므로, 애플리케이션에 대한 요청을 실행할 때마다 트레이스와 일련의 스팬이 생성됩니다. 데이터를 탐색할 수 있도록 애플리케이션에 대한 트래픽이 생성되고 있습니다.

1. **[Service Management > Software Catalog](https://app.datadoghq.com/services?env=progressive&hostGroup=)** 로 이동합니다. 
   그러면 Software Catalog의 **Ownership(소유권)** 탭이 열립니다.
1. **Reliability(신뢰성)** 탭을 클릭하여 분산 트레이싱에서 식별된
   Storedog 서비스 목록을 확인합니다.

Datadog Software Catalog에서는 조직에서 사용 중인 모든 서비스의 중요 정보를 한곳에서 확인할 수 있습니다. 엔드 투 엔드 서비스 소유권을 대규모로 구현하고, 실시간 성능 인사이트를 확보하며, 신뢰성 및 보안 리스크를 빠르게 감지하여 대응하고, 애플리케이션 종속성을 효율적으로 관리하는 등 이 모든 작업을 한곳에서 해결할 수 있습니다. Slack과 같은 팀 커뮤니케이션 도구, GitHub와 같은 소스 제어 도구, Datadog 대시보드, 그리고 각 서비스의 원격 분석 데이터를 수신하고 모니터링하는 Datadog 뷰를 이용할 수 있습니다.

> [!NOTE]
> 서비스를 별도로 연동하지 않아도 Software Catalog에 서비스가 표시됩니다. 메타데이터는 해당 정보가 포함된 YAML 파일을 업로드하여 추가할 수 있습니다. 자세한 내용은 [Software Catalog](https://docs.datadoghq.com/software_catalog/)에 대한 설명서에서 확인하세요.

![Service List(서비스 목록) 페이지 스크린샷](../assets/service_list.png)

어떤 서비스가 표시되나요? 각 서비스마다 어떤 정보를 얻을 수 있나요?

1. **Map(맵)**을 클릭하면 같은 정보가 좀 더 시각적인 형태로 표시됩니다. 환경 선택기가 
`env:progressive`로 설정되어 있어야 합니다.

Service Map(서비스 맵)은 애플리케이션 내에서 어떤 서비스가 서로 통신하는지 파악하는 데 유용합니다. 이 시각화된 정보가 표시되는 데는 몇 분 정도 걸릴 수 있으므로, 비어 있다면 교육 과정을 진행하면서 나중에 다시 확인해보시기 바랍니다. 정보가 채워지면 아래 그래프와 비슷한 형태로 표시됩니다.

![Service Map(서비스 맵) 페이지 스크린샷](../assets/service_map.png)

서비스 위에 마우스를 올려 트래픽과 지연 시간을 확인하세요.

마무리
===

위에서 언급한 Datadog 섹션을 충분히 살펴보셨으면 터미널에 다음 명령을 입력하세요.

```sh,run
finish
```

실습의 오른쪽 하단에 있는 **Check(확인)** 버튼을 클릭하고 결과가 표시될 때까지 기다리세요. 그런 후 실습 프레임 아래에 있는 **Next(다음)** 버튼을 선택하여 다음 섹션으로 계속 진행하세요.
