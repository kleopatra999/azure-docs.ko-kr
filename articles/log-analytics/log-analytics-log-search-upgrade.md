---
title: "새 로그 검색으로 Azure Log Analytics 업그레이드 | Microsoft Docs"
description: "새로운 Log Analytics 쿼리 언어가 곧 시작될 예정이며, 공개 미리 보기로 참여할 수 있습니다.  이 문서는 새 언어의 장점과 작업 영역을 변환하는 방법에 대해 설명합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte;bwren
ms.translationtype: HT
ms.sourcegitcommit: 7456da29aa07372156f2b9c08ab83626dab7cc45
ms.openlocfilehash: 4a3ee3c4d1fa9b626a51f24997603adceed8311f
ms.contentlocale: ko-kr
ms.lasthandoff: 08/28/2017

---

# <a name="upgrade-your-azure-log-analytics-workspace-to-new-log-search"></a>새 로그 검색으로 Azure Log Analytics 작업 영역 업그레이드

> [!NOTE]
> 새 Log Analytics 쿼리 언어로의 업그레이드는 현재 선택적으로 제공되어 [새 언어로 향상시킬 수 있습니다](https://go.microsoft.com/fwlink/?linkid=856078).  

새로운 Log Analytics 쿼리 언어가 이제 시작됩니다. 이를 활용하기 위해서는 작업 영역을 업그레이드해야 합니다.  이 문서는 새 언어의 장점과 작업 영역을 변환하는 방법에 대해 설명합니다.  지금 업그레이드를 선택하지 않고 예전과 동일하게 작업 영역을 진행하는 경우에도 나중에 자동으로 변환될 예정입니다.  해당 날짜가 정해지면 뜻 깊은 시간과 알림을 받게 될 것입니다.

이 문서는 새로운 언어와 업그레이드 프로세스에 관한 자세한 정보를 제공합니다.

## <a name="why-the-new-language"></a>왜 새로운 언어일까요?
모든 전환에는 수고스러움이 있고 단지 즐거움을 위해 쿼리 언어를 변경하는 것이 아닙니다.  이 변경이 Log Analytics 고객에게 중요한 가치를 제공하는 몇 가지 이유가 있습니다.

- **단순하면서도 강력합니다.** 새 언어에는 레거시 언어에 비해 더 자연어와 가까운 구조의 SQL과 유사하며 이해하기가 더 쉽습니다.
- **전체 파이핑 언어입니다.**  새 언어는 레거시 언어에 비해 더욱 광범위한 파이핑 기능이 있습니다.  사실상 모든 출력을 다른 명령으로 파이프하여 기존에 가능했던 것보다 더 복잡한 쿼리를 만들 수 있습니다.
- **검색-시간 필드 추출.**  새 언어는 기존 언어에 비해 한 차원 더 높은 런타임 계산 필드를 지원합니다.  확장된 필드에 대한 복잡한 계산을 사용할 수 있으며 조인 및 집계를 포함하는 추가 명령에 대해 계산 필드를 사용할 수 있습니다.
- **고급 조인.**  새 언어는 여러 필드에 테이블을 조인하고 내부 및 외부 조인을 사용하며 확장된 필드에 조인하는 기능을 포함하는 레거시 언어에 비해 더 고급 수준의 조인을 제공합니다.
- **날짜/시간 함수.**  새로운 언어는 레거시 언어에 비해 더 고급 수준의 날짜/시간 함수를 갖추고 있습니다.
- **스마트 분석.**  새 언어에는 데이터 집합의 패턴을 평가하고 다양한 데이터 집합을 비교하는 고급 알고리즘이 있습니다.
- **고급 분석 포털.**  고급 분석 포털은 쿼리, 추가 시각화 및 고급 진단의 여러 줄 편집을 포함하는 Log Analytics 포털에서 사용할 수 없는 분석 기능을 제공합니다.
- **다른 응용 프로그램과의 일관성.**  새로운 언어와 고급 분석 포털은 이미 Application Insights에서 분석에 사용됩니다.  Log Analytics에 대한 구현은 Azure 서비스 전반에 걸쳐 일관성을 제공합니다.
- **Power BI와의 더 나은 통합.** 새 언어로 된 쿼리를 Power BI Desktop에 내보내어 다양한 데이터 변환 기능을 활용할 수 있습니다.
- **그 외 더 많은 요소들이 있습니다.** [Azure Log Analytics 쿼리 언어](https://docs.loganalytics.io) 사이트에서 새로운 언어에 대한 전체 세부 정보 및 자습서를 참조하세요.


## <a name="when-can-i-upgrade"></a>언제 업그레이드할 수 있습니까?
업그레이드는 모든 Azure 지역에 걸쳐 출시될 예정이므로 일부 지역은 먼저 제공될 수도 있습니다.  작업 영역 위쪽에 업그레이드로 초대하는 보라색 배너가 보이면 작업 영역을 업그레이드할 수 있게 된 것입니다.

![업그레이드 1](media/log-analytics-log-search-upgrade/upgrade-01a.png)

## <a name="what-happens-when-i-upgrade"></a>업그레이드하면 어떻게 되나요?
작업 영역을 변환하는 경우 뷰 디자이너를 사용하여 만든 모든 저장된 검색, 경고 규칙 및 뷰는 새 언어로 자동으로 변환됩니다.  솔루션에 포함된 검색은 자동으로 변환되지 않지만, 사용자가 열면 그때그때 변환됩니다.  이러한 과정은 사용자가 인식하지 못합니다.

## <a name="can-i-go-back-after-i-upgrade"></a>업그레이드 후에 다시 돌아갈 수 있습니까?
업그레이드하면 작업 영역의 전체 백업이 수행되며, 모든 저장된 검색, 경고 규칙 및 뷰에 대한 스냅숏을 포함합니다.  그러면 나중에 원하는 경우 이전 작업 영역을 복원할 수 있습니다.

레거시 작업 영역을 복원하려면 작업 영역에서 **설정**, **업그레이드 요약**으로 이동합니다.  **레거시 작업 영역 복원**에 대한 옵션을 선택할 수 있습니다.  

![레거시 복원](media/log-analytics-log-search-upgrade/restore-legacy-b.png)

## <a name="how-do-i-perform-the-upgrade"></a>업그레이드를 수행하려면 어떻게 해야 합니까?
포털의 위쪽에 보라색 배너가 표시되면 작업 영역을 업그레이드할 수 있습니다.  

1.  **자세히 알아보고 업그레이드**라는 보라색 배너를 클릭하여 업그레이드 프로세스를 시작합니다.<br>![업그레이드 2](media/log-analytics-log-search-upgrade/upgrade-01a.png)<br>
2.  업그레이드 정보 페이지에서 업그레이드에 관한 추가 정보를 자세히 읽어보세요.<br>![업그레이드 2](media/log-analytics-log-search-upgrade/upgrade-03.png)<br>
3.  **지금 업그레이드**를 클릭하여 업그레이드를 시작합니다.<br>![업그레이드 4](media/log-analytics-log-search-upgrade/upgrade-04.png)<br>오른쪽 위 모서리에 알림 상자에 상태가 표시됩니다.<br>![업그레이드 5](media/log-analytics-log-search-upgrade/upgrade-05.png)
4.  끝났습니다.  로그 검색 페이지로 이동하여 업그레이드된 작업 영역을 살펴보세요.<br>![업그레이드 6](media/log-analytics-log-search-upgrade/upgrade-06.png)<br>

문제가 발생하여 업그레이드에 실패한 경우 [토론 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights)으로 이동하여 질문을 게시하거나 Azure Portal에서 [지원 요청을 만들](../azure-supportability/how-to-create-azure-support-request.md) 수 있습니다.

## <a name="how-do-i-learn-the-new-language"></a>새 언어를 어떻게 배울 수 있나요?
여러 서비스에서 사용될 때부터 새 언어에 대한 [설명서를 호스트 하는 외부 사이트](https://docs.loganalytics.io/)를 만들었습니다.  여기에는 속도를 개선하는 데 도움이 되는 자습서, 샘플 및 전체 참조가 포함되어 있습니다. [쿼리 시작](https://go.microsoft.com/fwlink/?linkid=856078)에서 새 언어에 대한 자습서를 진행하고, [Log Analytics 쿼리 언어](https://go.microsoft.com/fwlink/?linkid=856079)에서 언어 참조에 액세스할 수 있습니다.  

이미 레거시 Log Analytics 쿼리 언어에 대해 잘 알고 있는 경우 업그레이드의 일환으로 작업 영역에 추가되는 언어 변환기를 사용할 수 있습니다.

레거시 쿼리로 입력한 다음 **변환**을 클릭하기만 하면 번역된 버전을 볼 수 있습니다.  검색 단추를 클릭하여 검색을 실행하거나, 변환된 쿼리를 복사하고 붙여넣어 경고 규칙같이 다른 곳에서 사용할 수 있습니다.

![언어 변환기](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="next-steps"></a>다음 단계
- [새로운 언어에 관한 자습서](https://go.microsoft.com/fwlink/?linkid=856078)를 확인해 보세요.
- 새로운 쿼리 언어를 사용하여 [로그 검색 포털을 사용한 자습서](log-analytics-log-search-log-search-portal.md)를 진행해 보세요.
- 새로운 [고급 분석 포털](https://go.microsoft.com/fwlink/?linkid=856587)에 관해 알아보세요.

