---
title: "SQL Server 가상 컴퓨터 프로비전 | Microsoft Docs"
description: "포털을 사용하여 Azure에서 SQL Server 가상 컴퓨터를 만들고 연결하기. 이 자습서는 리소스 관리자 모드를 사용합니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: jroth
ms.translationtype: HT
ms.sourcegitcommit: b309108b4edaf5d1b198393aa44f55fc6aca231e
ms.openlocfilehash: c923f9aae4c7a1b8bd4f5760d0ec4f33923b9321
ms.contentlocale: ko-kr
ms.lasthandoff: 08/15/2017

---
# <a name="provision-a-sql-server-virtual-machine-in-the-azure-portal"></a>Azure Portal에서 SQL Server 가상 컴퓨터 프로비저닝
> [!div class="op_single_selector"]
> * [포털](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
> 
> 

이 종단간 자습서는 Azure Portal을 사용하여 SQL Server를 실행하는 가상 컴퓨터를 프로비전하는 방법을 보여줍니다.

Azure 가상 컴퓨터(VM) 갤러리에는 Microsoft SQL Server가 포함된 몇 개의 이미지가 있습니다. 클릭 몇 번으로, 갤러리에서 SQL VM 이미지 중 하나를 선택하고 Azure 환경에 프로비전할 수 있습니다.

이 자습서에서는 다음을 수행합니다.

* [갤러리에서 SQL VM 이미지 선택](#select-a-sql-vm-image-from-the-gallery)
* [VM 구성 및 만들기](#configure-the-vm)
* [원격 데스크톱을 사용하여 VM 열기](#open-the-vm-with-remote-desktop)
* [원격으로 SQL Server 연결](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-the-gallery"></a>갤러리에서 SQL VM 이미지 선택

1. 사용자 계정을 사용하여 [Azure Portal](https://portal.azure.com)에 로그인합니다.

   > [!NOTE]
   > Azure 계정이 없는 경우 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 방문하십시오.

2. Azure Portal에서 **새로 만들기**를 클릭합니다. 포털에 **새** 창이 열립니다.

3. **새로 만들기** 창에서 **Compute**를 클릭한 다음 **모두 표시**를 클릭합니다.

   ![새 계산 창](./media/virtual-machines-windows-portal-sql-server-provision/azure-new-compute-blade.png)

4. 검색 필드에 **SQL Server**를 입력하고 ENTER 키를 누릅니다.

5. 그런 다음, **필터** 아이콘을 클릭하고 게시자로 **Microsoft**를 선택합니다. 필터 창에서 **완료**를 클릭하여 결과를 Microsoft 게시 SQL Server 이미지로 필터링합니다.

   ![Azure Virtual Machines 창](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. 사용 가능한 SQL Server 이미지를 검토합니다. 각 이미지는 SQL Server 버전 및 운영 체제를 식별합니다.

6. **무료 라이선스: Windows Server 2016에서 SQL Server 2016 SP1 Developer**용 이미지를 선택합니다.

   > [!TIP]
   > Developer 버전은 개발 테스트 목적으로 무료로 제공되는 SQL Server의 모든 기능을 갖춘 버전이므로 이 자습서에서 사용됩니다. VM 실행 비용에 대해서만 비용을 지불합니다. 그러나 이 자습서에 사용할 이미지를 자유롭게 선택할 수 있습니다.

   > [!TIP]
   > SQL VM 이미지는 만든 VM의 분당 가격에 SQL Server에 대한 라이선스 비용을 포함합니다(Developer 및 Express 버전 제외). SQL Server Developer는 개발/테스트(비 프로덕션)에 대해 무료이며 SQL Express는 간단한 작업(1GB 미만의 메모리, 10GB 미만의 저장소)에 대해 무료입니다. BYOL(Bring Your Own License) 및 VM에 대해서만 지불에 대한 또 다른 옵션이 있습니다. 이러한 이미지 이름에는 접두사 {BYOL}이 붙습니다. 
   >
   > 이러한 옵션에 대한 자세한 내용은 [SQL Server Azure VM에 대한 가격 책정 지침](virtual-machines-windows-sql-server-pricing-guidance.md)을 참조하세요.

7. **배포 모델 선택**에서 **리소스 관리자**가 선택되어 있는지 확인합니다. 리소스 관리자는 새로운 가상 컴퓨터에 권장되는 배포 모델입니다. 

8. **만들기**를 클릭합니다.

    ![리소스 관리자로 SQL VM 만들기](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-the-vm"></a>VM 구성
SQL Server 가상 컴퓨터를 구성하기 위한 5개의 창이 있습니다.

| 단계 | 설명 |
| --- | --- |
| **기본 사항** |[기본 설정 구성](#1-configure-basic-settings) |
| **크기** |[가상 컴퓨터 크기 선택](#2-choose-virtual-machine-size) |
| **설정** |[선택적 기능 구성](#3-configure-optional-features) |
| **SQL 서버 설정** |[SQL Server 설정 구성](#4-configure-sql-server-settings) |
| **요약** |[요약 검토](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a>1. 기본 설정 구성

**기본** 창에서 다음 정보를 제공합니다.

* 고유한 가상 컴퓨터 **이름**을 입력합니다.

* 최적의 성능을 위해 VM 디스크 유형에 **SSD**를 선택합니다.

* VM의 로컬 관리자 계정에 대한 **사용자 이름**을 지정합니다. 이 계정은 SQL Server **sysadmin** 고정 서버 역할에도 추가됩니다.

* 강력한 **암호**를 제공합니다.

* 구독이 여러 개인 경우 구독이 새 VM에 대해 올바른지 확인합니다.

* **리소스 그룹** 상자에 새 리소스 그룹의 이름을 입력합니다. 또는 기존 리소스 그룹을 사용하려면 **기존 항목 사용**을 클릭합니다. 리소스 그룹은 Azure 내 관련 리소스의 컬렉션입니다(가상 컴퓨터, 저장소 계정, 가상 네트워크 등).

  > [!NOTE]
  > 새 리소스 그룹을 사용하면 Azure에서 SQL Server 배포를 테스트하거나 알아보는 경우에 유용합니다. 테스트를 완료한 후 리소스 그룹을 삭제하면 VM과 해당 리소스 그룹과 연결된 모든 리소스가 자동으로 삭제됩니다. 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../../../azure-resource-manager/resource-group-overview.md)를 참조하세요.

* 이 배포를 호스팅할 Azure 지역에 **위치**를 선택합니다.

* **확인**을 클릭하여 설정을 저장합니다.

    ![SQL 기본 창](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a>2. 가상 컴퓨터 크기 선택

**크기** 단계의 **크기 선택** 창에서 가상 컴퓨터 크기를 선택합니다. 창은 선택한 이미지를 기반으로 권장되는 컴퓨터 크기를 처음에 표시합니다.

> [!IMPORTANT]
> **크기 선택** 창에 표시된 월별 예상 비용에는 SQL Server 라이선스 비용이 포함되지 않습니다. 이것은 VM만의 비용입니다. SQL Server의 Express 및 Developer 버전의 경우, 이것은 총 예상 비용입니다. 다른 버전의 경우 [Windows Virtual Machines 가격 책정 페이지](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)를 참조하여 SQL Server의 대상 버전을 선택하세요. 또한 [SQL Server Azure VM에 대한 가격 책정 지침](virtual-machines-windows-sql-server-pricing-guidance.md)을 참조하세요.

![SQL VM 크기 옵션](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

프로덕션 워크로드의 경우 [Azure Virtual Machines의 SQL Server에 대한 성능 모범 사례](virtual-machines-windows-sql-performance.md)에서 권장하는 컴퓨터 크기 및 구성을 참조하세요. 나열되지 않은 컴퓨터 크기가 필요할 경우 **모든 보기** 단추를 클릭하세요.

> [!NOTE]
> 가상 컴퓨터 크기에 대한 자세한 내용은 [가상 컴퓨터 크기](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.

컴퓨터 크기를 선택한 다음 **선택**을 클릭합니다.

## <a name="3-configure-optional-features"></a>3. 선택적 기능 구성

**설정** 창에서 가상 컴퓨터용 Azure Storage, 네트워킹 및 모니터링을 구성합니다.

* **Storage**의 **Managed Disks**에서 **예**를 선택합니다.

   > [!NOTE]
   > SQL Server에 Managed Disks를 사용하는 것이 좋습니다. Managed Disks는 배후에서 저장소를 처리해줍니다. 또한 Managed Disks가 있는 가상 컴퓨터가 동일한 가용성 집합에 속할 경우 Azure는 저장소 리소스를 배포하여 적절한 중복성을 제공합니다. 자세한 내용은 [Azure Managed Disks 개요](../../../storage/storage-managed-disks-overview.md)를 참조하세요. 가용성 집합의 Managed Disks에 대한 구체적인 내용을 보려면 [가용성 집합에서 VM에 Managed Disks 사용](../manage-availability.md)을 참조하세요.

* **네트워크**아래에서 자동으로 채워진 값을 사용할 수 있습니다. 각 기능을 클릭하여 **가상 네트워크**, **서브넷**, **공용 IP 주소** 및 **네트워크 보안 그룹**을 수동으로 구성할 수도 있습니다. 이 자습서에서는 기본 값을 유지합니다.

* Azure에서는 VM에 지정된 것과 동일한 저장소 계정을 통해 **모니터링**이 기본적으로 사용됩니다. 여기에서 이러한 설정을 변경할 수 있습니다.

* **가용성 집합**에서 이 자습서에 대해 기본값을 **없음**으로 남겨둘 수 있습니다. SQL AlwaysOn 가용성 그룹을 설정하려는 경우 가상 컴퓨터를 다시 만들지 않도록 가용성을 구성합니다.  자세한 내용은 [Virtual Machines의 가용성 관리](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.

이러한 설정 구성을 완료한 후 **확인**을 클릭합니다.

## <a name="4-configure-sql-server-settings"></a>4. SQL Server 설정 구성
**SQL Server 설정** 창에서 SQL Server에 대한 설정 및 최적화를 구성합니다. SQL Server에 대해 구성할 수 있는 설정은 다음과 같습니다.

| 설정 |
| --- |
| [연결](#connectivity) |
| [인증](#authentication) |
| [Storage 구성](#storage-configuration) |
| [자동화된 패치](#automated-patching) |
| [자동화된 Backup](#automated-backup) |
| [Azure Key Vault 통합](#azure-key-vault-integration) |
| [R 서비스](#r-services) |

### <a name="connectivity"></a>연결

**SQL 연결**에서 VM의 SQL Server 인스턴스에 대해 원하는 액세스 유형을 지정합니다. 이 자습서에서는 **공개(인터넷)**를 지정하여 인터넷 상의 컴퓨터 또는 서비스에서 SQL Server로의 연결을 허용합니다. 이 옵션을 선택하면 Azure에서는 포트 1433에서 트래픽을 허용하도록 방화벽 및 네트워크 보안 그룹을 자동으로 구성합니다.

![SQL 연결 옵션](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

> [!TIP]
> 기본적으로 SQL Server는 잘 알려진 포트 **1433**에서 수신 대기합니다. 보안 향상을 위해 이전 대화 상자의 포트를 기본 이외 포트(예: 1401)를 수신하도록 변경하세요. 이 작업을 수행할 경우 SSMS와 같이 모든 클라이언트 도구의 해당 포트를 사용하여 연결해야 합니다.

인터넷을 통해 SQL Server에 연결하려면 SQL Server 인증을 사용하도록 설정해야 합니다. 이 내용은 다음 섹션에 설명되어 있습니다.

인터넷을 통해 데이터베이스 엔진에 대한 연결을 사용하도록 설정하지 않으려면 다음 옵션 중 하나를 선택합니다.

* **로컬(VM 내부만)**을 선택합니다.
* **사설(Virtual Network 내)**을 선택합니다.

일반적으로, 시나리오에 허용되는 가장 제한적인 연결을 선택하여 보안을 개선합니다. 하지만 모든 옵션은 네트워크 보안 그룹 및 SQL/Windows 인증을 통해 보안을 설정할 수 있습니다. VM이 만들어진 후에 네트워크 보안 그룹을 편집할 수 있습니다. 자세한 내용은 [Azure Virtual Machines의 SQL Server에 대한 보안 고려 사항](virtual-machines-windows-sql-security.md)을 참조하세요.

> [!NOTE]
> SQL Server Express Edition용 가상 컴퓨터 이미지는 자동으로 TCP/IP 프로토콜을 사용하지 않습니다. 공용 및 개인 연결 옵션에 대해서도 마찬가지입니다. Express Edition의 경우 VM을 만든 후에 SQL Server 구성 관리자를 사용하여 [수동으로 TCP/IP 프로토콜을 사용](#configure-sql-server-to-listen-on-the-tcp-protocol) 해야 합니다.

### <a name="authentication"></a>인증

SQL Server 인증이 필요하도록 지정하려면 **사용** under **사용**을 방문하십시오.

![SQL Server 인증](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> 인터넷(즉, 공용 연결 옵션)을 통해 SQL Server에 액세스하려는 경우 여기에서 SQL 인증을 사용해야 합니다. SQL Server에 대한 공용 액세스를 위해서는 SQL 인증을 사용해야 합니다.
> 
> 

SQL Server 인증을 사용하도록 설정하는 경우 **로그인 이름** 및 **암호**를 지정합니다. 이 사용자 이름은 SQL Server 인증 로그인 및 **sysadmin** 고정된 서버 역할의 구성원으로 구성됩니다. 인증 모드에 대한 자세한 내용은 [인증 모드 선택](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode)을 참조하세요.

SQL Server 인증을 사용하도록 설정하지 않으면, VM의 로컬 관리자 계정을 사용하여 SQL Server 인스턴스에 연결할 수 있습니다.

### <a name="storage-configuration"></a>Storage 구성

저장소 요구 사항을 지정하려면 **Storage 구성**을 클릭합니다.

![SQL Storage 구성](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> 표준 저장소를 사용하도록 VM을 수동으로 구성한 경우 이 옵션은 사용할 수 없습니다. 자동 저장소 최적화는 Premium Storage에서만 사용할 수 있습니다.

> [!TIP]
> 정지 수와 각 슬라이더의 상한값은 사용자가 선택한 VM 크기에 따라 다릅니다. 더 크고 효율적인 VM이 추가 확장할 수 있습니다.

초당 입/출력 작업(IOPs), 처리량(MB/s) 및 총 저장소 크기로 요구 사항을 지정할 수 있습니다. 슬라이딩 규모를 사용하여 이 값을 구성합니다. 워크로드에 따라 이러한 저장소 설정을 변경할 수 있습니다. 포털에는 이러한 요구 사항에 따라 장착 및 구성할 디스크 수를 자동으로 계산합니다.

**다음에 대해 Storage 최적화**에서 다음 옵션 중 하나를 선택합니다.

* **일반**은 기본 설정이며 대부분의 워크로드를 지원합니다.
* **트랜잭션** 처리는 기존의 데이터베이스 OLTP 워크로드용으로 저장소를 최적화합니다.
* **데이터 웨어하우징**은 분석 및 보고 워크로드용으로 저장소를 최적화합니다.

### <a name="automated-patching"></a>자동화된 패치

**Automated patching**이 사용됩니다. Azure에서는 자동화된 패치를 통해 SQL Server와 운영 체제를 자동으로 패치합니다. 요일, 시간 및 유지 관리 기간에 대한 날짜를 지정합니다. Azure에서 유지 관리 기간에 패치를 수행합니다. 유지 관리 기간 일정에서는 VM 로캘 시간을 사용합니다. Azure에서 SQL Server와 운영 체제를 자동으로 패치하지 않으려면 **사용 안 함**을 클릭합니다.  

![SQL 자동화된 패치](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

자세한 내용은 [Azure Virtual Machines에서 SQL Server의 자동화된 패치](virtual-machines-windows-sql-automated-patching.md)를 참조하세요.

### <a name="automated-backup"></a>자동화된 백업

**자동화된 백업**에서 모든 데이터베이스에 대해 자동 데이터베이스 백업을 사용하도록 설정합니다. 자동화된 백업은 기본적으로 사용하지 않도록 설정됩니다.

SQL 자동화된 백업을 사용하면 다음을 구성할 수 있습니다.

* 백업에 대한 보존 기간(일)
* 백업에 사용할 저장소 계정
* 백업을 위한 암호화 옵션 및 암호
* 시스템 데이터베이스 백업
* 백업 일정 구성

백업을 암호화하려면 **사용**을 클릭합니다. 그 다음 **암호**를 지정합니다. Azure에서는 백업을 암호화할 인증서를 만들고 지정된 암호를 사용하여 인증서를 보호합니다.

![SQL 자동화된 Backup](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 자세한 내용은 [Azure Virtual Machines에서 SQL Server에 대한 자동화된 Backup](virtual-machines-windows-sql-automated-backup.md)을 참조하세요.

### <a name="azure-key-vault-integration"></a>Azure Key Vault 통합

Azure에서 암호화를 위한 보안 암호를 저장하려면 **Azure Key Vault 통합**을 클릭하고 **사용**을 클릭합니다.

![SQL Azure Key Vault 통합](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

다음 표에서는 Azure Key Vault 통합을 구성하는 데 필요한 매개 변수를 나열합니다.

| 매개 변수 | 설명 | 예제 |
| --- | --- | --- |
| **주요 자격 증명 모음 URL** |주요 자격 증명 모음의 위치입니다. |https://contosokeyvault.vault.azure.net/ |
| **주체 이름** |Azure Active Directory 서비스 주체 이름. 이 이름을 클라이언트 ID라고도 합니다. |fde2b411-33d5-4e11-af04eb07b669ccf2 |
| **주체 암호** |Azure Active Directory 서비스 주체 암호입니다. 이 암호를 클라이언트 암호라고도 합니다. |9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM= |
| **자격 증명 이름** |**자격 증명 이름**: AKV 통합은 VM이 주요 자격 증명 모음에 액세스할 수 있도록 SQL Server 내에 자격 증명을 만듭니다. 이 자격 증명의 이름을 선택하세요. |mycred1 |

자세한 내용은 [Azure VM에서 SQL Server에 대한 Azure Key Vault 통합 구성](virtual-machines-windows-ps-sql-keyvault.md)을 참조하세요.

### <a name="r-services"></a>R 서비스

[SQL Server R 서비스](https://msdn.microsoft.com/library/mt604845.aspx)를 사용하도록 설정하는 옵션이 있습니다. SQL Server 2016을 사용하여 고급 분석을 사용할 수 있습니다. **SQL Server 설정** 창에서 **사용**을 클릭합니다.

> [!NOTE]
> SQL Server 2016 Developer Edition의 경우 이 옵션이 포털에서 잘못 비활성화되어 있습니다. Developer 버전의 경우 VM을 생성한 후 R 서비스를 수동으로 활성화해야 합니다.

![SQL Server R 서비스 사용](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)

SQL Server 설정 구성을 마치면 **확인**을 클릭합니다.

## <a name="5-review-the-summary"></a>5. 요약 검토

**요약** 창에서 요약을 검토하고 **구매**를 클릭하여 이 VM에 대해 지정된 SQL Server, 리소스 그룹 및 리소스를 만듭니다.

Azure Portal에서 배포를 모니터링할 수 있습니다. 화면 맨 위에 있는 **알림** 단추는 배포의 기본 상태를 표시합니다.

> [!NOTE]
> 배포 시간에 대한 정보를 제공하기 위해 SQL VM을 미국 동부 지역에 기본 설정을 사용하여 배포해 두었습니다. 이 테스트 배포는 완료하기까지 총 26분이 소요되었습니다. 사용자의 지역 및 선택한 설정에 따라서 배포 시간이 더 빠르거나 늦을 수 있습니다.

## <a name="open-the-vm-with-remote-desktop"></a>원격 데스크톱을 사용하여 VM 열기

다음 단계를 사용하여 원격 데스크톱으로 SQL Server 가상 컴퓨터에 연결합니다.

> [!INCLUDE [Connect to SQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

SQL Server 가상 컴퓨터에 연결된 후에, SQL Server Management Studio를 시작하고 로컬 관리자 자격 증명을 사용하여 Windows 인증으로 연결할 수 있습니다. SQL Server 인증을 사용하도록 설정한 경우에는, 프로비전 중에 구성해 놓은 SQL 로그인 및 암호를 사용하여 SQL 인증에 연결할 수 있습니다.

컴퓨터에 연결하면 요구 사항에 따라 컴퓨터와 SQL Server 설정을 직접 변경할 수 있습니다. 예를 들어, 방화벽 설정을 구성하거나 SQL Server 구성 설정을 변경할 수 있습니다.

## <a name="enable-tcpip-for-developer-and-express-editions"></a>개발자 및 Express 버전에 대해 TCP/IP 사용

새 SQL Server VM을 프로비전할 때 Azure는 SQL Server 개발자 및 Express 버전에 대해 TCP/IP 프로토콜을 자동으로 설정하지 않습니다. 아래 단계에서는 IP 주소를 통해 원격으로 연결할 수 있도록 TCP/IP를 수동으로 사용하도록 설정하는 방법을 설명합니다.

다음 단계에서는 **SQL Server 구성 관리자**를 사용하여 SQL Server 개발자 및 Express 버전에 대해 TCP/IP 프로토콜을 사용하도록 설정합니다.

> [!INCLUDE [Connect to SQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-to-sql-server-remotely"></a>원격으로 SQL Server 연결

이 자습서에서는 가상 컴퓨터와 **SQL Server 인증**에 대해 **공용** 액세스를 선택했습니다. 이러한 설정은 가상 컴퓨터가 인터넷을 통한 모든 클라이언트의 SQL Server 연결을 허용하도록 자동으로 구성합니다(올바른 SQL 로그인이 있다는 가정 하에).

> [!NOTE]
> 프로비전 중에 공용을 선택하지 않은 경우 프로비전 후 포털을 통해 SQL 연결 설정을 변경할 수 있습니다. 자세한 내용은 [SQL 연결 설정 변경](virtual-machines-windows-sql-connect.md#change)을 참조하세요.

다음 섹션은 인터넷 상의 다른 컴퓨터에서 VM의 SQL Server 인스턴스에 연결하는 방법을 보여줍니다.

> [!INCLUDE [Connect to SQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a>다음 단계

Azure에서 SQL Server를 사용하는 방법에 대한 기타 정보는 [Azure Virtual Machines의 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md) 및 [질문과 대답](virtual-machines-windows-sql-server-iaas-faq.md)을 참조하세요.
