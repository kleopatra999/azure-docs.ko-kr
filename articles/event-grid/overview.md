---
title: "Azure Event Grid 개요"
description: "Azure Event Grid 및 해당 개념을 설명합니다."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.translationtype: HT
ms.sourcegitcommit: 847eb792064bd0ee7d50163f35cd2e0368324203
ms.openlocfilehash: 59a834f32793e349d5639baf3c80dbcba274dfa8
ms.contentlocale: ko-kr
ms.lasthandoff: 08/19/2017

---

# <a name="an-introduction-to-azure-event-grid"></a>Azure Event Grid 소개

Azure Event Grid를 사용하면 이벤트 기반 아키텍처를 가진 응용 프로그램을 쉽게 빌드할 수 있습니다. 구독할 Azure 리소스를 선택하고, 이벤트를 전송하는 이벤트 처리기 또는 웹후크 끝점을 제공합니다. Event Grid는 기본적으로 저장소 Blob 및 리소스 그룹과 같은 Azure 서비스의 이벤트를 지원합니다. 또한 Event Grid는 사용자 지정 토픽 및 사용자 지정 웹후크를 사용하여 응용 프로그램 및 타사 이벤트에 대한 사용자 지정을 지원합니다. 

필터를 사용하여 다른 끝점에 대한 특정 이벤트를 라우팅하고, 여러 끝점으로 멀티캐스트하며, 이벤트가 안정적으로 배달되도록 할 수 있습니다. Event Grid에는 기본적으로 사용자 지정 및 타사 이벤트를 지원합니다.

미리 보기 릴리스의 경우 Event Grid는 **westus2** 및 **westcentralus** 위치를 지원합니다. 다른 지역이 추가됩니다.

이 문서는 Azure Event Grid의 개요를 제공합니다. Event Grid를 시작하려는 경우 [Azure Event Grid를 사용하여 사용자 지정 이벤트 만들기 및 라우팅](custom-event-quickstart.md)을 참조하세요.

![Event Grid 기능 모델](./media/overview/event-grid-functional-model.png)

현재, Blob Storage는 게시자로 공개적으로 사용할 수 없습니다.

## <a name="concepts"></a>개념

이제부터 살펴볼 Azure Event Grid의 5가지 개념은 다음과 같습니다.

* **이벤트** - 발생한 내용입니다.
* **이벤트 원본/게시자** - 이벤트가 발생한 곳입니다.
* **토픽** - 게시자가 이벤트를 보낸 끝점입니다.
* **이벤트 구독** - 때때로 여러 처리기에 이벤트를 라우팅하는 끝점 또는 기본 제공 메커니즘입니다. 구독도 처리기가 지능적으로 들어오는 이벤트를 필터링하는 데 사용됩니다.
* **이벤트 처리기** - 이벤트에 반응하는 앱 또는 서비스입니다.

이러한 개념에 대한 자세한 내용은 [Azure Event Grid의 개념](concepts.md)을 참조하세요.

## <a name="capabilities"></a>기능

Azure Event Grid의 몇 가지 주요 기능은 다음과 같습니다.

* **단순성** - Azure 리소스부터 모든 이벤트 처리기 또는 끝점의 이벤트를 목표로 선택하고 클릭합니다.
* **고급 필터링** - 이벤트 처리기가 관련 이벤트만 수신하도록 이벤트 형식 또는 이벤트 게시자 경로를 필터링합니다.
* **팬 아웃** - 필요에 따라 다양한 위치로 이벤트 사본을 보낼 수 있도록 동일한 이벤트에 대한 여러 끝점을 구독합니다.
* **안정성** - 이벤트 배달을 보장하기 위해 지수 백오프를 통한 다시 시도를 24시간 사용합니다.
* **이벤트별 요금** - Event Grid를 사용하는 만큼만 지불합니다.
* **높은 처리량** - 초당 수백만 개 이벤트 지원을 통해 Event Grid에서 대량 워크로드를 빌드합니다.
* **기본 제공 이벤트** - 리소스 정의 기본 제공 이벤트를 사용하여 신속하게 준비하고 실행합니다.
* **사용자 지정 이벤트** - Event Grid를 사용하여 사용자 앱의 사용자 지정 이벤트를 라우팅하고, 필터링하며, 안정적으로 배달합니다.

## <a name="built-in-publisher-and-handler-integration"></a>기본 제공 게시자 및 처리기 통합

Azure는 게시자 및 처리기를 모두 포함한 다양한 서비스를 사용하는 기본 제공 이벤트 지원을 제공합니다.

### <a name="publishers"></a>게시자

현재 다음 Azure 서비스는 Event Grid에 대한 기본 제공 게시자를 지원합니다.

* 리소스 그룹(관리 작업)
* Azure 구독(관리 작업)
* Event Hubs
* 사용자 지정 토픽

올해 다른 Azure 서비스가 추가될 예정입니다.

### <a name="handlers"></a>처리기

현재 다음 Azure 서비스는 Event Grid에 대한 기본 제공 처리기를 지원합니다. 

* Azure 기능
* Logic Apps
* Azure Automation
* 웹후크

올해 다른 Azure 서비스가 추가될 예정입니다.

## <a name="what-can-i-do-with-event-grid"></a>Event Grid로 할 수 있는 작업은 무엇인가요?

Azure Event Grid는 서버를 사용하지 않는 작업 자동화 및 통합 작업을 크게 개선하는 여러 기능을 제공합니다. 

### <a name="serverless-application-architectures"></a>서버를 사용하지 않는 응용 프로그램 아키텍처

![서버를 사용하지 않는 응용 프로그램](./media/overview/serverless_web_app.png)

Event Grid는 데이터 원본과 이벤트 처리기를 연결합니다. 예를 들어 Event Grid를 사용하여, 새 사진이 Blob Storage 컨테이너에 추가될 때마다 이미지 분석을 실행하도록 서버를 사용하지 않는 함수를 즉시 트리거합니다. 

### <a name="ops-automation"></a>작업 자동화

![작업 자동화](./media/overview/Ops_automation.png)

Event Grid를 통해 자동화를 가속화하고 정책 적용을 간소화할 수 있습니다. 예를 들어 Event Grid는 가상 컴퓨터가 만들어지거나 SQL Database가 실행되면 Azure Automation에 알릴 수 있습니다. 이러한 이벤트는 서비스 구성이 준수 상태인지 자동으로 확인하고 메타데이터를 작업 도구에 배치하고 가상 컴퓨터에 태그를 지정하거나 작업 항목을 제출하는 데 사용될 수 있습니다.

### <a name="application-integration"></a>응용 프로그램 통합

![응용 프로그램 통합](./media/overview/app_integration.png)

Event Grid는 앱을 다른 서비스와 연결합니다. 예를 들어 앱의 이벤트 데이터를 Event Grid로 보내고 Event Grid의 안정적인 배달, 고급 라우팅 및 Azure와의 직접 통합을 활용하는 사용자 지정 토픽을 만듭니다. 또는 Event Grid와 Logic Apps를 사용하여, 코드를 작성할 필요 없이 어디서든 데이터를 처리할 수 있습니다. 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a>Event Grid는 다른 Azure 통합 서비스와 어떻게 다릅니까?

Event Grid는 이벤트 구동, 반응성 프로그래밍을 사용할 수 있는 이벤트 백플레인입니다. Azure 서비스와 긴밀히 통합하고 타사 서비스와 통합할 수 있습니다. 이벤트 메시지는 서비스 및 응용 프로그램의 변화에 대응하는 데 필요한 정보를 포함합니다. Event Grid는 데이터 파이프라인이 아니며, 업데이트된 실제 개체를 배달하지 않습니다.

Service Bus는 트랜잭션, 순서 지정, 중복 검색 및 즉시 일관성을 필요로 하는 일반적인 엔터프라이즈 응용 프로그램에 적합합니다. Event Grid는 반응성 모델의 속도, 비율 크기 조정, 너비 및 저렴한 비용을 위해 고안되었습니다. 서버를 사용하지 않는 아키텍처에 적합합니다.

Event Grid는 Logic Apps 및 Event Hubs와 같은 다른 Azure 서비스를 보완합니다. Event Grid는 해당 워크플로를 시작하기 위해 논리 앱을 트리거합니다. Event Hubs는 Event Hubs 캡처 이벤트에 대응하고 데이터 수신과 변환 파이프라인을 빌드할 수 있도록 Event Grid와 작동합니다.

## <a name="how-much-does-event-grid-cost"></a>Event Grid의 비용은 얼마입니까?

Azure Event Grid는 이벤트별 요금 가격 책정 모델을 사용하므로 사용한 것에 대해서만 지불하면 됩니다.

Event Grid의 비용은 백만 작업당 $0.60(미리 보기 중 $0.30)이며, 매달 처음 100, 000개 작업은 무료입니다. 작업은 이벤트 수신, 고급 일치, 배달 시도 및 관리 호출로 정의됩니다.  자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/event-grid/)에서 찾을 수 있습니다.

## <a name="next-steps"></a>다음 단계

* [사용자 지정 이벤트 만들기 및 구독](custom-event-quickstart.md) Azure Event Grid 빠른 시작을 사용하여 사용자 지정 이벤트를 끝점으로 보내려면 바로 이동합니다.
* [Logic Apps를 이벤트 처리기로 사용](monitor-virtual-machine-changes-event-grid-logic-app.md) Event Grid에서 푸시된 이벤트에 대응하기 위해 Logic Apps를 사용하여 앱을 빌드하는 자습서입니다.
* [Event Grid REST API 참조](/rest/api/eventgrid)  
  Azure Event Grid에 대한 자세한 기술 정보 및 이벤트 구독 관리, 라우팅 및 필터링에 대한 참조를 제공합니다.
