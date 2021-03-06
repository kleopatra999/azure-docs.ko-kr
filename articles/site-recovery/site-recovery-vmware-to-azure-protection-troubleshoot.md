---
title: "VMware/물리적 서버에서 Azure로 보호 실패 문제 해결 | Microsoft Docs"
description: "이 문서에서는 일반적인 VMware 컴퓨터 복제 실패 및 이러한 문제를 해결하는 방법을 설명합니다."
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/26/2017
ms.author: asgang
ms.translationtype: Human Translation
ms.sourcegitcommit: 07584294e4ae592a026c0d5890686eaf0b99431f
ms.openlocfilehash: 6ebec2e06566b1e2d6834fdd81c0d8b2801b80b9
ms.contentlocale: ko-kr
ms.lasthandoff: 06/02/2017


---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a>온-프레미스 VMware/물리적 서버 복제 문제 해결
Azure Site Recovery를 사용하여 VMware 가상 컴퓨터 또는 물리적 서버를 보호하는 경우 특정 오류 메시지가 나타날 수 있습니다. 이 문서에서는 발생할 수 있는 일반적인 일부 오류 메시지와 이 문제를 해결하기 위한 문제 해결 단계에 대해 자세히 설명합니다.


## <a name="initial-replication-is-stuck-at-0"></a>초기 복제가 0%에 고정됩니다.
지원에서 발견하는 대부분의 초기 복제 실패는 원본 서버와 프로세스 서버 간 또는 프로세스 서버와 Azure 간의 연결 문제로 인한 것입니다.
대부분의 경우 아래 나열된 단계를 수행하여 이러한 문제를 자체 해결할 수 있습니다.

###<a name="check-the-following-on-source-machine"></a>원본 컴퓨터에서 다음을 확인
* 원본 서버 컴퓨터 명령줄에서 텔넷을 사용하여 아래와 같이 네트워크 연결 문제나 방화벽 포트 차단 문제가 있는지 https 포트(기본값 9443)로 프로세스 서버를 ping합니다.
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > 텔넷을 사용하고 PING을 사용하여 연결을 테스트하지 마십시오.  텔넷이 설치되지 않은 경우 [여기](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)에서 단계 목록을 따릅니다.

연결할 수 없는 경우 프로세스 서버에서 인바운드 포트 9443을 허용하고 문제가 여전히 있는지 확인합니다. 프로세스 서버가 DMZ 뒤에 있어서 이 문제를 일으켰던 경우도 있었습니다.

* 실행되지 않는 경우 서비스 `InMage Scout VX Agent – Sentinel/OutpostStart`의 상태를 확인하고 문제가 여전히 있는지 확인합니다.   
 
###<a name="check-the-following-on-process-server"></a>프로세스 서버에서 다음을 확인

* **프로세스 서버가 데이터를 Azure로 적극적으로 밀어넣는지 확인** 

프로세스 서버 컴퓨터에서 작업 관리자(Ctrl-Shift-Esc 키를 눌러)를 엽니다. 성능 탭으로 이동하고 ‘리소스 모니터 열기’ 링크를 클릭합니다. 리소스 관리자에서 네트워크 탭으로 이동합니다. '네트워크 작업을 사용하여 프로세스'의 cbengine.exe가 적극적으로 대량의(단위: Mb) 데이터를 보내는지 확인합니다.

![복제 활성화](./media/site-recovery-protection-common-errors/cbengine.png)

그렇지 않은 경우 아래 나열된 단계를 따르세요.

* **프로세스 서버가 Azure Blob에 연결할 수 있는지 확인**: 'TCP 연결'을 보도록 cbengine.exe를 선택하고 확인하여 프로세스 서버에서 Azure Storage Blob URL로 연결이 있는지 확인합니다.

![복제 활성화](./media/site-recovery-protection-common-errors/rmonitor.png)

그렇지 않은 경우 제어판 > 서비스로 이동하고 다음 서비스가 실행되고 있는지 확인합니다.

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
실행되지 않는 서비스를 (다시)시작하고 문제가 여전히 있는지 확인합니다.

* **프로세스 서버가 포트 443을 사용하여 Azure 공용 IP 주소에 연결할 수 있는지 확인**

`%programfiles%\Microsoft Azure Recovery Services Agent\Temp`에서 최신 CBEngineCurr.errlog를 열고 443 및 연결 시도 실패를 검색합니다.

![복제 활성화](./media/site-recovery-protection-common-errors/logdetails1.png)

문제가 있는 경우 프로세스 서버 명령줄에서 포트 443을 사용하여 CBEngineCurr.currLog에서 발견된 Azure 공용 IP 주소(위 이미지에 마스킹된)를 ping하도록 텔넷을 사용합니다.

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
연결할 수 없는 경우 다음 단계에 설명된 대로 액세스 문제가 방화벽 또는 프록시로 인한 것인지 확인합니다.


* **프로세스 서버의 IP 주소 기반 방화벽이 액세스를 차단하지 않는지 확인**: 서버에서 IP 주소 기반 방화벽 규칙을 사용하는 경우 [여기](https://www.microsoft.com/download/details.aspx?id=41653)에서 Microsoft Azure 데이터 센터 IP 범위의 전체 목록을 다운로드하고 방화벽 구성에 추가하여 Azure(및 HTTPS(443) 포트)에 대한 통신을 허용하도록 합니다.  구독하는 Azure 지역과 미국 서부에 해당하는 IP 주소 범위를 허용하세요(Access Control 및 ID 관리에 사용됨).

* **프로세스 서버의 URL 기반 방화벽이 액세스를 차단하지 않는지 확인**: 서버에서 URL 기반 방화벽 규칙을 사용하는 경우 다음 URL이 방화벽 구성에 추가되었는지 확인합니다. 
     
  `*.accesscontrol.windows.net:` - Access Control 및 Identity Management에 사용됨

  `*.backup.windowsazure.com:` - 복제 데이터 전송 및 오케스트레이션에 사용됨

  `*.blob.core.windows.net:` 복제된 데이터를 저장하는 저장소 계정에 액세스하는 데 사용됨

  `*.hypervrecoverymanager.windowsazure.com:` - 복제 관리 작업 및 오케스트레이션에 사용됨

  `time.nist.gov` 및 `time.windows.com`: 시스템 시간과 글로벌 시간 간의 시간 동기화를 확인하는 데 사용됨

**Azure Government 클라우드**의 URL:

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* **프로세스 서버의 프록시 설정이 액세스를 차단하지 않는지 확인합니다**.  프록시 서버를 사용하는 경우 DNS 서버에서 프록시 서버 이름을 확인하는지 확인합니다.
구성 서버 설치 시 제공한 것을 확인하려면 레지스트리 키로 이동합니다.

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

이제 Azure Site Recovery에서 데이터를 보내는 데 동일한 설정을 사용하는지 확인합니다.
Microsoft Azure Backup 검색 

![복제 활성화](./media/site-recovery-protection-common-errors/mab.png)

해당 항목을 열고 작업 > 속성 변경을 클릭합니다. 프록시 구성 탭 아래에 레지스트리 설정에 의해 표시된 것과 동일해야 하는 프록시 주소가 표시됩니다. 그렇지 않은 경우 동일한 주소로 변경하세요.

![복제 활성화](./media/site-recovery-protection-common-errors/mabproxy.png)

* **대역폭 제한이 프로세스 서버에서 제한되지 않는지 확인**: 대역폭을 늘리고 문제가 여전히 있는지 확인합니다.

##<a name="next-steps"></a>다음 단계
도움이 필요한 경우 [ASR 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr)에 쿼리를 게시합니다. 활발히 유지되는 커뮤니티가 있으며 엔지니어 중 하나가 도움을 줄 수 있습니다.
