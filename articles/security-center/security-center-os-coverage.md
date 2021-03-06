---
title: "Azure Security Center에서 지원되는 플랫폼 | Microsoft Docs"
description: "이 문서에서는 Azure Security Center에서 지원되는 Windows 및 Linux 운영 체제의 목록을 제공합니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.translationtype: Human Translation
ms.sourcegitcommit: ff2fb126905d2a68c5888514262212010e108a3d
ms.openlocfilehash: c33e132037d95fa92fd59a8243a9a8a351ae0224
ms.contentlocale: ko-kr
ms.lasthandoff: 06/17/2017


---
# <a name="supported-platforms-in-azure-security-center"></a>Azure Security Center에서 지원되는 플랫폼
클래식 및 Resource Manager 배포 모델을 모두 사용하여 작성된 VM(가상 컴퓨터)에 대해 보안 상태 모니터링 및 권장 사항이 제공됩니다.

> [!NOTE]
> Azure 리소스의 [클래식 및 리소스 관리자 배포 모델](../azure-classic-rm.md) 에 대해 자세히 알아봅니다.
>
>

## <a name="supported-platforms-for-windows-vms"></a>Windows VM에 대해 지원되는 플랫폼
지원되는 Windows 운영 체제:

* Windows Server 2008
* Windows Server 2008 R2
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

> [!NOTE]
>
* Windows Server 2016에는 아직 OS 취약성 평가를 사용할 수 없습니다.
* 충돌 분석 탐지는 Windows Server 2012 및 Windows Server 2012 R2에만 지원됩니다.
>
>

## <a name="supported-platforms-for-linux-vms"></a>Linux VM에 대해 지원되는 플랫폼
지원되는 Linux 운영 체제:

* Ubuntu 버전 12.04, 14.04, 16.04, 16.10
* Debian 버전 7, 8
* CentOS 버전 6.\*, 7.*
* RHEL(Red Hat Enterprise Linux) 버전 6.\*, 7.*
* SUSE Linux Enterprise Server(SLES) 버전 11 SP4+, 12.*
* Oracle Linux 버전 6.\*, 7.*

> [!NOTE]
> Linux 운영 체제에서는 아직 가상 컴퓨터 동작 분석을 사용할 수 없습니다.
>
>

## <a name="vms-and-cloud-services"></a>VM 및 Cloud Services
클라우드 서비스에서 실행 중인 VM도 지원됩니다. 프로덕션 슬롯에서 실행되는 클라우드 서비스 웹 및 작업자 역할만 모니터링됩니다. 클라우드 서비스에 대한 자세한 내용은 [클라우드 서비스 개요](../cloud-services/cloud-services-choose-me.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

- [Azure Security Center의 계획 및 운영 가이드](security-center-planning-and-operations-guide.md) — 디자인 고려 사항을 계획하고 이해하여 Azure Security Center를 채택하는 방법을 알아봅니다.
- [Azure Security Center에서 유형별 보안 경고](https://docs.microsoft.com/en-us/azure/security-center/security-center-alerts-type.md#virtual-machine-behavioral-analysis) - Security Center에서 가상 컴퓨터 동작 분석 및 크래시 덤프 메모리 분석에 대해 자세히 알아봅니다.
- [Azure 보안 센터 FAQ](security-center-faq.md) — 서비스 사용에 관한 질문과 대답을 찾습니다.
- [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) — Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.

