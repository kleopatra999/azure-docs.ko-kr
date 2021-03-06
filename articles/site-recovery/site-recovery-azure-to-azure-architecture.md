---
title: "Azure Site Recovery에서 Azure 지역 간에 Azure 가상 컴퓨터 복제가 작동하는 방식  | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery 서비스를 사용하여 Azure 지역 간에 Azure VM을 복제하는 경우 사용되는 구성 요소와 아키텍처에 대한 개요를 제공합니다."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/31/2017
ms.author: sujayt
ms.translationtype: Human Translation
ms.sourcegitcommit: db18dd24a1d10a836d07c3ab1925a8e59371051f
ms.openlocfilehash: ec397eaeda963f257d1bd996f1f57189bcde17ca
ms.contentlocale: ko-kr
ms.lasthandoff: 06/15/2017

---

# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a>Site Recovery에서 Azure VM 복제가 작동하는 방식


이 문서에서는 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 하나의 지역에서 다른 지역으로 Azure VM(가상 컴퓨터)을 복제하고 복구하는 데 관련되는 구성 요소와 프로세스에 대해 설명합니다.

>[!NOTE]
>Site Recovery 서비스를 사용하는 Azure VM 복제는 현재 미리 보기로 제공됩니다.

이 문서의 하단에서 의견을 게시하거나 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 질문하세요.

## <a name="architectural-components"></a>아키텍처 구성 요소

다음 다이어그램은 특정 지역(이 예제에서는 미국 동부 지역)의 Azure VM 환경을 개략적으로 보여 줍니다. Azure VM 환경은 다음과 같습니다.
- 앱은 여러 저장소 계정에 디스크가 분산되어 있는 VM에서 실행될 수 있습니다.
- VM은 가상 네트워크 내에서 하나 이상의 서브넷에 포함될 수 있습니다.

![고객 환경](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

[지원 매트릭스](site-recovery-support-matrix-azure-to-azure.md)에서 배포 필수 구성 요소 및 요구 사항을 알아보세요.

## <a name="replication-process"></a>복제 프로세스

### <a name="step-1"></a>1단계

Azure Portal에서 Azure VM 복제를 사용하는 경우 다음 다이어그램과 표에 표시된 리소스가 대상 지역에 자동으로 만들어집니다. 기본적으로 리소스는 원본 지역 설정을 기반으로 만들어집니다. 필요에 따라 대상 설정을 사용자 지정할 수 있습니다. [자세히 알아보세요](site-recovery-replicate-azure-to-azure.md)을 확인하세요.

![복제를 사용하도록 설정하는 프로세스, 1단계](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

**리소스** | **세부 정보**
--- | ---
**대상 리소스 그룹** | 장애 조치(failover) 후 복제된 VM이 속하게 되는 리소스 그룹입니다.
**대상 가상 네트워크** | 장애 조치(failover) 후 복제된 VM이 있는 가상 네트워크입니다. 네트워크 매핑은 원본 및 대상 가상 네트워크 간에 만들어집니다.
**캐시 저장소 계정** | 원본 VM에 대한 변경 내용은 대상 저장소 계정에 복제되기 전에 추적되어 대상 위치의 캐시 저장소 계정으로 전송됩니다. 이렇게 하면 VM에서 실행 중인 프로덕션 앱에 미치는 영향을 최소화합니다.
**대상 저장소 계정**  | 데이터가 복제되는 대상 위치의 저장소 계정입니다.
**대상 가용성 집합**  | 장애 조치(failover) 후 복제된 VM이 있는 가용성 집합입니다.

### <a name="step-2"></a>2단계

복제를 사용하도록 설정하면 Site Recovery 확장 이동성 서비스가 VM에 자동으로 설치됩니다. 다음 동작이 발생합니다.

1. VM이 Site Recovery에 등록됩니다.

2. VM에 대해 연속 복제가 구성됩니다. VM 디스크에서의 데이터 쓰기가 원본 위치의 캐시 저장소 계정에 지속적으로 전송됩니다.

   ![복제를 사용하도록 설정하는 프로세스, 2단계](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > Site Recovery에는 VM에 대한 인바운드 연결이 필요하지 않습니다. VM은 Site Recovery 서비스 URL/IP 주소, Office 365 인증 URL/IP 주소 및 캐시 저장소 계정 IP 주소에 대한 아웃바운드 연결만 필요합니다. 자세한 내용은 [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md)(Azure 가상 컴퓨터 복제를 위한 네트워킹 지침) 문서를 참조하세요.

## <a name="continuous-replication-process"></a>연속 복제 프로세스

연속 복제가 작동한 후에는 디스크 쓰기가 캐시 저장소 계정으로 즉시 전송됩니다. Site Recovery는 데이터를 처리하여 대상 저장소 계정으로 보냅니다. 데이터가 처리된 후에는 몇 분마다 대상 저장소 계정에 복구 지점이 생성됩니다.

## <a name="failover-process"></a>장애 조치(failover) 프로세스

장애 조치(failover)를 시작하면 대상 리소스 그룹, 대상 가상 네트워크, 대상 서브넷 및 대상 가용성 집합에 VM이 만들어집니다. 장애 조치(failover) 중에는 모든 복구 지점을 사용할 수 있습니다.

![장애 조치(failover) 프로세스](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a>다음 단계

- Azure VM 복제를 위한 [네트워킹](site-recovery-azure-to-azure-networking-guidance.md)에 대해 알아보세요.
- [Azure VM 복제](site-recovery-azure-to-azure.md)를 연습해 보세요.

