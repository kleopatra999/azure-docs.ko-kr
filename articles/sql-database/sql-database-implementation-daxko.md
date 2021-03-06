---
title: "Azure SQL Database Azure 사례 연구 - Daxko/CSI | Microsoft Docs"
description: "Daxko/CSI에서 SQL 데이터베이스를 사용하여 개발 주기를 가속화하고 고객 서비스 및 성능을 개선하는 방법을 알아봅니다."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 00c8a713-f20c-4d6b-b8b7-0c1b9ba5f05b
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.translationtype: Human Translation
ms.sourcegitcommit: 95b8c100246815f72570d898b4a5555e6196a1a0
ms.openlocfilehash: 61d62cde5311c8e447acf8890e0a32339585bb42
ms.contentlocale: ko-kr
ms.lasthandoff: 05/18/2017


---
# <a name="daxkocsi-used-azure-to-accelerate-its-development-cycle-and-to-enhance-its-customer-services-and-performance"></a>Daxko/CSI에서 Azure를 사용하여 개발 주기를 가속화하고 고객 서비스 및 성능 개선
![Daxko/CSI 로고](./media/sql-database-implementation-daxko/csidaxkologo25.png)

Daxko/CSI Software는 한 가지 문제에 직면해 있습니다. 이 기업에서는 포괄적인 엔터프라이즈 소프트웨어 솔루션의 성공 덕분에 피트니스 및 레크리에이션 센터의 고객 기반이 빠르게 증가하고 있지만 증가하는 고객 기반의 IT 인프라 요구를 충족하기 위해 회사의 IT 직원을 테스트하고 있습니다. 이 회사는 특히 증가하는 데이터베이스 관리를 위한 운영 오버헤드 증가로 압박을 받고 있습니다. 더 나쁜 점은 운영 오버헤드 때문에 새 이니셔티브(예: 회사 소프트웨어에 대한 새로운 모바일 기능)를 위한 개발 리소스가 감소하고 있다는 것이었습니다.

Daxko/CSI의 제품 개발 책임자인 David Molina에 따르면, Azure는 데이터베이스 관리를 간소화하고, 확장성을 높이고, ops 대신 소프트웨어에만 집중하도록 리소스를 확보하는 데 필요한 PaaS(platform-as-a-service) 모델로 CSI 소프트웨어를 제공했습니다. "Azure SQL 데이터베이스는 우리에게 아주 유용한 선택 옵션이었습니다. SQL Server, 장애 조치 클러스터 및 다른 모든 인프라를 유지 관리하는 문제를 걱정할 필요가 없다는 점은 매우 이상적인 것이었습니다."

Azure로 마이그레이션한 이후에 CSI Software는 600개가 넘는 고객 데이터베이스를 관리하기 위해 2명의 작업 담당자만 필요합니다. 이 회사는 Azure SQL 데이터베이스의 탄력적 풀을 사용하여 크기 및 필요에 따라 고객 데이터베이스를 이동합니다.

“우리 고객은 변화가 시급하다고 느겼습니다. 탄력적 풀 이전에는 버스트 기간 동안 제한 시간 및 기타 문제가 가끔씩 발생했습니다. Azure의 탄력적 풀을 사용하면서 필요에 따라 버스트되며, 문제 없이 소프트웨어를 사용할 수 있게 되었습니다."라고 Molina는 덧붙였습니다.

고객을 위한 성능 개선 외에도, Azure의 탄력적 풀은 작업 및 관리를 처리하는 대신 새로운 서비스 및 기능을 개발하는 데 주력하기 위해 CSI Software 리소스를 확보합니다. 이러한 IT 리소스는 CSI Software에서 엔터프라이즈 소프트웨어 제품인 SpectrumNG를 개선하여 체육관 회원을 모집하고, 직원 효율성을 높이고, 직원과 회원들이 대화형 작업 및 실시간 알림에 모바일로 액세스할 수 있도록 합니다.

또한 Azure는 CSI Software가 자동화 옵션을 활용하여 개발 및 QA(품질 보증) 주기를 가속화하고 개선하도록 도와주었습니다. 회사의 Azure 구현을 통해, 빌드 관리자는 단추 클릭만으로 구성 요소를 패키징할 수 있습니다. "이제 릴리스 주기에 속하는 QA를 통해 Azure에서 테스트 환경을 배포할 수 있습니다. 이 환경은 프로덕션 스택과 매우 유사합니다. 개발 환경에 빌드를 즉시 배포하여 변화를 검사할 수 있습니다. 이전에는 테스트를 위한 이러한 공간이 없었으므로 이점은 큰 도움이 되었습니다."라고 Molina는 설명했습니다.

## <a name="offloading-to-the-cloud"></a>클라우드로 오프로드
CSI Software는 클라우드로 이동하기 전에 휴스턴에 있는 로컬 데이터 센터에서 자체적인 다중 테넌트 인프라를 구축했습니다. 이 회사는 확장되면서 고객을 지원하는 데 필요한 모든 소프트웨어 및 하드웨어를 구매, 프로비전 및 유지 관리하는 과정에서 많은 어려움에 직면했습니다. 작업 처리를 위한 IT 인력 배치도 또 다른 병목 현상이 되었습니다. 이로 인해 새 리소스를 프로비전하고 새로운 서비스를 고객에게 롤아웃하는 시간이 느려졌습니다.

CSI Software에서는 이러한 오버헤드를 없애고 작업 자체가 아닌 코드에 집중할 수 있도록 하기 위한 클라우드 옵션을 알아보게 되었습니다. 이 회사는 많은 주요 클라우드 공급자가 IaaS(Infrastructure-as-a-Service) 솔루션만 제공하고 있다는 것을 알게 되었습니다. IaaS 스택을 관리하려면 여전히 많은 수의 IT 직원이 필요합니다. 결국 CSI Software는 Azure PaaS 솔루션이 요구에 가장 잘 맞는다는 결론을 내렸습니다. "Azure에서는 하드웨어 및 시스템 소프트웨어에 대해 신경쓸 필요가 없으므로 IT 오버헤드를 줄이면서 소프트웨어 제품이 집중할 수 있습니다."라고 Molina는 설명했습니다.

## <a name="making-the-transition-to-azure"></a>Azure로의 전환 수행
CSI Software는 PaaS 솔루션을 위해 Azure를 선택한 후 해당 백 엔드 인프라 및 데이터베이스를 클라우드로 마이그레이션하기 시작했습니다. Azure를 사용하기 전에, SpectrumNG 고객은 WCF(Windows Communication Foundation) 서비스와 통신하는 클라이언트 응용 프로그램을 백 엔드에 설치해야 했습니다. Molina에 따르면 "일부 고객은 자체 데이터 센터에 모든 항목을 호스트하고 있지만 우리는 제품을 다중 테넌트로 빌드했습니다. 모든 항목을 휴스턴에 있는 데이터 센터에 호스트하고, 데이터 저장소로 SQL Server를 사용했습니다.

우리의 제품에도 회원용 웹 포털(ASP.net으로 작성)이 포함되어 있습니다. 이 포털은 고객의 웹 서비스와 일치하도록 흰색으로 레이블링되고 온라인 페이지 및 타사 통합을 모두 지원하기 위해 SOAP API로 디자인되었습니다."

클라우드로의 마이그레이션을 아키텍처에 비해 오래 걸리지 않았습니다. Molina에 따르면 "주로 구성 파일 정보를 읽는 방식, 중앙 집중식 연결 문자열 수정 및 릴리스의 패키징, 업로드 및 배포 자동화에 노력을 지울였습니다.”

빌드 자동화를 개발하기 위해 CSI Software 엔지니어는 Azure PowerShell 및 REST API를 사용하여 패키지를 만든 후, 매일 밤 릴리스를 위한 스테이징 환경에 업로드했습니다.
CSI Software IT 팀 입장에서 Azure 클라우드 기반 배포로의 전반적인 전환은 빠르고 원활하게 진행되었습니다. "우리는 결국 프로젝트에 착수하고 3~4주 안에 클라우드에 베타 환경을 구축할 수 있게 되었습니다. 정말 놀라운 성과였습니다.”라고 Molina는 설명했습니다.

CSI Software는 환경을 구성 및 테스트한 후 고객 마이그레이션을 시작했습니다. 이미 CSI Software 호스팅을 사용하는 고객의 경우 전환이 거의 원활하게 진행되었습니다. 온-프레미스 배포에서 마이그레이션하는 고객의 경우, 클라우드로의 마이그레이션에는 추가 시간이 소요되지만, 고객과 CSI Software 둘 다 큰 문제가 없었습니다.

새 고객을 위해 CSI Software의 IT 직원들은 다음 프로세스를 사용하여 Azure에 온보드합니다.

1. Azure PowerShell 스크립트는 고객에 대한 새 데이터베이스를 스핀업하는 데 사용됩니다. 모든 고객은 전환을 위해 충분한 초기 처리량을 보장하도록 프리미엄 계층에서 시작합니다.
2. 가능한 경우 CSI Software는 Azure SQL 마이그레이션 마법사를 사용하여 기존 데이터를 Azure SQL 데이터베이스 인스턴스로 이동합니다.
3. 마지막으로 데이터의 불일치를 조정하거나 필요에 따라 데이터 정리를 수행하기 위해 Microsoft SSIS(SQL Server Integration Services)가 사용됩니다.

현재, CSI Software 고객의 약 99%가 4개의 지역 데이터 센터(중북부, 중남부, 동부, 서부)에 있는 Azure에 호스트되고 있습니다. 각 고객의 지리적 지역에 데이터 센터를 배치함으로써 대기 시간을 최소한으로 유지합니다.

## <a name="azure-elastic-pools-free-up-it-resources"></a>Azure 탄력적 풀로 IT 리소스 확보
Azure의 일부 기능은 CSI Software가 인프라 및 운영에 집중하지 않고 기능 및 개발에 집중하도록 도와주었습니다. 아마도 가장 큰 장점은 탄력적 풀을 통해 구현되었을 것입니다.

CSI Software는 현재 고객에게 약 550개의 데이터베이스를 제공합니다. 탄력적 풀 전에는 계층 구조 내에서 이렇게 많은 데이터베이스를 관리하는 것이 어려웠습니다. ops 관리자는 상당한 양의 IT 리소스 오버헤드를 요구하는 고객의 폭발적인 요구를 토대로 성능 계층을 할당해야 했습니다. 탄력적 풀을 사용하면서 관리자들은 테넌트에 프리미엄 또는 표준 풀을 적절히 할당한 다음 크기 및 필요에 따라 고객을 이동할 수 있습니다. 고객은 탄력적 풀의 효과를 거의 즉시 느꼈습니다. 탄력적 풀을 사용하기 전에는 버스트 사용 기간 동안 시간 제한 및 기타 문제가 발생했지만 탄력적 풀을 사용하게 되면서 필요에 따라 활동 버스트를 경험하게 되고, SpectrumNG를 문제 없이 계속 사용할 수 있게 되었습니다.

## <a name="azure-active-geo-replication-accelerates-reporting"></a>Azure 활성 지역 복제로 보고 기능 가속화
일부 CSI Software 고객은 Azure 활성 지역 복제도 활용하고 있습니다. 활성 지역 복제를 사용하면 동일하거나 다른 데이터 센터 지역에서 최대 4개의 읽기 기능한 보조 데이터베이스를 구성할 수 있습니다. CSI Software는 두 가지 방법으로 활성 지역 복제를 사용합니다. 첫 번째는 데이터 센터 가동 중단이 발생하거나 주 데이터베이스에 연결할 수 없는 경우 보조 데이터베이스를 사용할 수 있다는 것입니다. 두 번째는 보조 데이터베이스를 읽을 수 있으며, 보고 작업과 같은 읽기 전용 워크로드를 오프로드하는 데 사용할 수 있다는 것입니다. 일부 CSI Software 고객은 이러한 장점을 이용하여 보고 워크플로를 가속화합니다.

## <a name="csi-software-application-logic-and-architecture"></a>CSI Software 응용 프로그램 논리 및 아키텍처
SpectrumNG에서는 웹 역할을 사용합니다. 응용 프로그램이 다중 테넌트이기 때문에 WCF 서비스를 사용하여 고객의 초기 연결 요청을 처리합니다. "요청은 각 고객을 식별하며, 연결 문자열을 데이터베이스로 빌드함으로써 수행해야 하는 작업을 수행하도록 합니다."라고 Molina는 설명했습니다.

해당 서비스의 웹 계층의 경우, CSI Software는 날짜 및 시간에 따라 Azure 자동 크기 조정을 활용합니다. 사용 가능한 리소스는 각 지역 데이터 센터의 표준 시간대에 따라 업무 시간 동안 더 높은 사용량에 맞게 자동으로 증가됩니다. 고객의 요구가 감소하면 주말에 리소스 규모를 줄이도록 설정됩니다.

![Daxko/CSI 아키텍처](./media/sql-database-implementation-daxko/figure1.png)

그림 1. 클라우드 서비스 작업자 역할은 Azure SQL 데이터베이스에서 구조화된 데이터를 가져오고, 테이블 저장소에서 반구조화된 데이터를 가져옵니다. SpectrumNG 사용자는 클라우드 데이터 서비스 웹 역할을 통해 해당 데이터와 상호 작용합니다.

## <a name="using-web-apps-and-a-web-plan-tier-for-mobile-apps"></a>모바일 앱에 대해 웹앱 및 웹 계획 계층 사용
Azure SQL 데이터베이스를 사용하면 리소스가 확보되므로 CSI Software에서 Azure 웹앱에 호스트되는 사용자 지정 API를 기반으로 하는 완벽한 모바일 플랫폼을 비롯한 새로운 이니셔티브를 구현할 수 있게 되었습니다. 이 플랫폼은 체육관 회원 및 직원들이 모바일 장치를 사용하여 일정을 확인하고, 수업을 예약하고, 메시지를 받도록 합니다.

이 플랫폼은 모든 항목을 원래 웹 계획에 그대로 두면서, SOA(서비스 지향 아키텍처)를 사용하여 단일 구성 요소(예: POS(Point-of-Sale) 시스템 또는 판매 시스템)를 받아들이고, 즉석에서 다른 웹 계획으로 이동한 다음 서비스를 스핀업하여 해당 구성 요소를 지원합니다. 이 기능은 CSI Software에 놀라운 유연성을 제공하고, 비용 절감에도 도움을 줍니다.

## <a name="azure-lets-csi-software-developers-focus-on-apps-and-services"></a>Azure를 통해 CSI Software 개발자가 앱 및 서비스에 집중
Azure SQL 데이터베이스는 빠르고 안정적인 서비스를 즐기는 SpectrumNG에게 유용한 기능일뿐 아니라 CSI Software의 IT 직원 및 개발자에게 큰 행운이기도 했습니다. CSI Software는 ops를 클라우드의 Azure에 오프로드하여, 리소스 및 인프라에 대한 오버헤드를 줄이고, 해당 개발 주기를 획기적으로 가속화하고, 테넌트에 맞게 성능을 최적화하기 위해 더 이상 데이터베이스를 세부적으로 관리할 필요가 없게 되었습니다.

## <a name="more-information"></a>자세한 정보
* Azure의 탄력적 풀에 대한 자세한 내용은 [탄력적 풀](sql-database-elastic-pool.md)을 참조하세요.
* 데이터베이스 도구 및 탄력적 크기 조정에 대한 자세한 내용은 [탄력적 데이터베이스 도구 및 탄력적 크기 조정](sql-database-elastic-scale-get-started.md)을 참조하세요.
* SQL Server 데이터베이스 마이그레이션에 대한 자세한 내용은 [Azure에 SQL Server 데이터베이스 마이그레이션](sql-database-cloud-migrate.md)을 참조하세요.
* 활성 지역 복제에 대한 자세한 내용은 [활성 지역 복제](sql-database-geo-replication-overview.md)를 참조하세요.
* 웹 역할 및 작업자 역할에 대한 자세한 내용은 [작업자 역할](../fundamentals-introduction-to-azure.md#compute)을 참조하세요.    
* Azure 서비스 버스에 대한 자세한 내용은 [Azure 서비스 버스](https://azure.microsoft.com/services/service-bus/)를 참조하세요.
* 자동 크기 조정에 대한 자세한 내용은 [클라우드 서비스 크기 조정](../cloud-services/cloud-services-how-to-scale.md)을 참조하세요.


