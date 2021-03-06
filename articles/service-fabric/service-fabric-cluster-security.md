---
title: "Service Fabric 클러스터 보안 | Microsoft Docs"
description: "서비스 패브릭 클러스터에 대한 보안 시나리오와 이러한 시나리오를 구현하는 데 사용되는 여러 다양한 기술에 대해 설명합니다."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 26b58724-6a43-4f20-b965-2da3f086cf8a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: chackdan
ms.translationtype: HT
ms.sourcegitcommit: 54774252780bd4c7627681d805f498909f171857
ms.openlocfilehash: 5afbe575a8affc37b8f902c0988585a83921e3d2
ms.contentlocale: ko-kr
ms.lasthandoff: 07/28/2017

---
# <a name="service-fabric-cluster-security-scenarios"></a>서비스 패브릭 클러스터 보안 시나리오
서비스 패브릭 클러스터는 사용자가 소유하는 리소스입니다. 실행 중인 프로덕션 작업이 있을 때 권한 없는 사용자가 클러스터에 연결하지 못하도록 하여 클러스터의 보안을 유지해야 합니다. 보안이 되지 않은 클러스터를 만들 수 있지만, 이렇게 하면 공용 인터넷에 관리 끝점이 노출될 경우 익명 사용자가 클러스터에 연결할 수 있게 됩니다. 

이 문서에서는 Azure 또는 독립 실행형에서 실행되는 클러스터에 대한 보안 시나리오의 개요와 이러한 시나리오를 구현하는 데 사용되는 다양한 기술에 대해 설명합니다. 클러스터 보안 시나리오:

* 노드 간 보안
* 클라이언트-노드 보안
* RBAC(역할 기반 액세스 제어)

## <a name="node-to-node-security"></a>노드 간 보안
클러스터의 VM 또는 컴퓨터 간 통신을 보호합니다. 이렇게 하면 클러스터에 가입하도록 인증된 컴퓨터만 호스팅 응용 프로그램 및 클러스터의 서비스에 참여할 수 있습니다.

![노드-노드 통신의 다이어그램][Node-to-Node]

Azure에서 실행되는 클러스터 또는 Windows에서 실행되는 독립 실행형 클러스터는 Windows Server 컴퓨터에 대한 [인증서 보안](https://msdn.microsoft.com/library/ff649801.aspx) 또는 [Windows 보안](https://msdn.microsoft.com/library/ff649396.aspx)을 사용할 수 있습니다.

### <a name="node-to-node-certificate-security"></a>노드 간 인증서 보안
서비스 패브릭은 클러스터를 만들 때 노드 유형 구성의 일부로 지정하는 X.509 서버 인증서를 사용합니다. 인증서 정보 및 인증서 획득 또는 생성 방법에 대한 빠른 개요는 이 문서의 끝에 제공됩니다.

Azure 포털, Azure Resource Manager 템플릿 또는 독립 실행형 JSON 템플릿을 통해 클러스터를 만드는 동안 인증서 보안이 구성됩니다. 기본 인증서 및 인증서 롤오버에 사용되는 선택적 보조 인증서를 지정할 수 있습니다. 지정한 기본 및 보조 인증서는 관리 클라이언트 및 [클라이언트-노드 보안](#client-to-node-security)에 대해 지정한 읽기 전용 클라이언트 인증서와 다릅니다.

Azure의 경우 클러스터에서 인증서 보안을 구성하는 방법을 알아보려면 [Azure Resource Manager 템플릿을 사용하여 클러스터 설정](service-fabric-cluster-creation-via-arm.md) 을 참조하세요.

독립 실행형 Windows Server의 경우 [X.509 인증서를 사용하여 Windows에서 독립 실행형 클러스터 보안 ](service-fabric-windows-cluster-x509-security.md)

### <a name="node-to-node-windows-security"></a>노드 간 Windows 보안
독립 실행형 Windows Server의 경우 [Windows 보안을 사용하여 Windows에서 독립 실행형 클러스터 보안](service-fabric-windows-cluster-windows-security.md)

## <a name="client-to-node-security"></a>클라이언트-노드 보안
클라이언트를 인증하고 클라이언트와 클러스터의 개별 노드 간 통신을 보호합니다. 이 보안 유형은 클라이언트 통신을 인증 및 보호하여 인증된 사용자만 클러스터 및 클러스터에 배포된 응용 프로그램에 액세스할 수 있도록 합니다. 클라이언트는 Windows 보안 자격 증명이나 인증서 보안 자격 증명을 통해 고유하게 식별됩니다.

![클라이언트-노드 통신의 다이어그램][Client-to-Node]

Azure에서 실행되는 클러스터 또는 Windows에서 실행되는 독립 실행형 클러스터는 [인증서 보안](https://msdn.microsoft.com/library/ff649801.aspx) 또는 [Windows 보안](https://msdn.microsoft.com/library/ff649396.aspx)을 사용할 수 있습니다.

### <a name="client-to-node-certificate-security"></a>클라이언트-노드 인증서 보안
 클라이언트-노드 인증서 보안은 관리 클라이언트 인증서 및/또는 사용자 클라이언트 인증서를 지정하여 Azure 포털, Resource Manager 템플릿 또는 독립 실행형 JSON 템플릿을 통해 클러스터를 만드는 동안 구성됩니다.  모범 사례에서는 지정한 관리 클라이언트 인증서 및 사용자 클라이언트 인증서가 [노드 간 보안](#node-to-node-security)용으로 지정한 기본 및 보조 인증서와 달라야 합니다. 기본적으로 노드 간 보안용 클러스터 인증서는 허용된 클라이언트 관리자 인증서 목록에 추가됩니다.

관리 인증서를 사용하여 클러스터에 연결하는 클라이언트에는 관리 기능에 대한 모든 권한이 있습니다.  읽기 전용 사용자 클라이언트 인증서를 사용하여 클러스터에 연결하는 클라이언트는 관리 기능에 대한 읽기 전용 액세스 권한만 있습니다. 즉, 이러한 인증서는 이 문서 뒷부분에 설명된 RBAC(역할 기반 액세스 제어)에 사용됩니다.

Azure의 경우 클러스터에서 인증서 보안을 구성하는 방법을 알아보려면 [Azure Resource Manager 템플릿을 사용하여 클러스터 설정](service-fabric-cluster-creation-via-arm.md) 을 참조하세요.

독립 실행형 Windows Server의 경우 [X.509 인증서를 사용하여 Windows에서 독립 실행형 클러스터 보안 ](service-fabric-windows-cluster-x509-security.md)

### <a name="client-to-node-azure-active-directory-aad-security-on-azure"></a>Azure에서 클라이언트-노드 AAD(Azure Active Directory) 보안
Azure에서 실행되는 클라이언트는 AAD(Azure Active Directory)를 사용하여 관리 끝점에 안전하게 액세스할 수 있습니다. 필요한 AAD 아티팩트를 만드는 방법, 클러스터를 만들 때 이러한 아티팩트를 채우는 방법 및 나중에 해당 클러스터에 연결하는 방법에 대한 자세한 내용은 [Azure Resource Manager 템플릿을 사용하여 클러스터 설정](service-fabric-cluster-creation-via-arm.md) 을 참조하세요.

## <a name="security-recommendations"></a>보안 권장 사항
Azure 클러스터의 경우 AAD 보안을 사용하여 노드 간 보안에 대해 클라이언트 및 인증서를 인증하는 것이 좋습니다.

독립 실행형 Windows Server 클러스터의 경우 Windows Server 2012 R2 및 Active Directory가 있는 경우 GMA(그룹 관리 계정)로 Windows 보안을 사용하는 것이 좋습니다. 그렇지 않은 경우 여전히 Windows 계정으로 Windows 보안을 사용합니다.

## <a name="role-based-access-control-rbac"></a>RBAC(역할 기반 액세스 제어)
액세스 제어를 사용하면 클러스터 관리자가 사용자 그룹마다 특정 클러스터 작업에 대한 액세스를 제한하여 클러스터의 보안을 강화할 수 있습니다. 클러스터에 연결하는 클라이언트에 대해 두 가지 액세스 제어 유형인 관리자 역할 및 사용자 역할이 지원됩니다.

관리자는 관리 기능(읽기/쓰기 기능만 포함)에 대한 모든 권한을 가집니다. 사용자는 기본적으로 관리 기능(예: 쿼리 기능)에 대한 읽기 권한 및 응용 프로그램과 서비스를 확인하는 기능만 갖습니다.

클러스터를 만들 때 각각에 대해 개별 ID(인증서, AAD 등)를 제공하여 관리자 및 사용자 클라이언트 역할을 지정합니다. 기본 액세스 제어 설정 및 기본 설정을 변경하는 방법에 대한 자세한 내용은 [Service Fabric 클라이언트에 대한 역할 기반 액세스 제어](service-fabric-cluster-security-roles.md)를 참조하세요.

## <a name="x509-certificates-and-service-fabric"></a>X.509 인증서 및 서비스 패브릭
X.509 디지털 인증서는 클라이언트 및 서버를 인증하고 암호화하고 디지털로 메시지를 서명하는 데 일반적으로 사용됩니다. 이러한 인증서에 대한 자세한 내용은 [인증서 작업](http://msdn.microsoft.com/library/ms731899.aspx)으로 이동합니다.

고려할 몇 가지 중요한 사항은 다음과 같습니다.

* 프로덕션 워크로드를 실행하는 클러스터에 사용되는 인증서는 올바르게 구성된 Windows Server 인증서 서비스를 사용하여 만들어지거나 승인된 [CA(인증 기관)](https://en.wikipedia.org/wiki/Certificate_authority)에서 획득해야 합니다.
* 프로덕션 환경에서 MakeCert.exe와 같은 도구를 사용하여 만든 임시 또는 테스트 인증서를 사용하지 마세요.
* 자체 서명된 인증서를 사용할 수 있지만 프로덕션이 아닌 테스트 클러스터에 대해서만 이러한 인증서를 사용해야 합니다.

### <a name="server-x509-certificates"></a>서버 X.509 인증서
서버 인증서에는 서버(노드)에서 클라이언트 또는 서버(노드)에서 서버(노드)로 인증의 주요 작업이 있습니다. 클라이언트 또는 노드가 노드를 인증할 때 초기 검사 중 하나는 제목 필드에 있는 일반 이름의 값을 확인하는 것입니다. 이 일반 이름 또는 인증서 주체 대체 이름 중 하나는 허용된 일반 이름 목록에 있어야 합니다.

다음 문서는 SAN(주체 대체 이름)을 사용하여 인증서를 생성하는 방법에 대해 설명합니다. [보안 LDAP 인증서에 주체 대체 이름을 추가하는 방법](http://support.microsoft.com/kb/931351)

주체 필드에는 값 형식을 나타내는 이니셜로 접두사가 붙은 여러 값이 포함될 수 있습니다. 가장 일반적으로 이니셜은 일반 이름에 대해 "CN"이며 예를 들어 "CN = www.contoso.com"입니다. 주체 필드를 비워둘 수도 있습니다. 선택적 주체 대체 이름 필드가 채워진 경우 인증서의 일반 이름과 주체 대체 이름당 하나의 항목을 모두 포함해야 합니다. 이러한 작업은 DNS 이름 값으로 입력됩니다.

인증서의 용도 필드의 값은 "서버 인증" 또는 "클라이언트 인증"과 같은 적절한 값을 포함해야 합니다.

### <a name="client-x509-certificates"></a>클라이언트 X.509 인증서
클라이언트 인증서는 일반적으로 타사 인증 기관에서 발급되지 않습니다. 대신 현재 사용자 위치의 개인 저장소는 일반적으로 "클라이언트 인증"의 목적으로 루트 인증 기관에서 넣은 클라이언트 인증서를 포함합니다. 상호 인증이 필요한 경우 클라이언트에서 이러한 인증서를 사용할 수 있습니다.

> [!NOTE]
> 서비스 패브릭 클러스터의 모든 관리 작업은 서버 인증서가 필요합니다. 관리에 클라이언트 인증서를 사용할 수 없습니다.
> 
> 

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->


## <a name="next-steps"></a>다음 단계
이 문서에서는 클러스터 보안에 대한 개념 정보를 제공합니다. 다음으로,


1.  [Resource Manager 템플릿을 사용하여 Azure에 클러스터 만들기](service-fabric-cluster-creation-via-arm.md) 
2.  [Azure Portal](service-fabric-cluster-creation-via-portal.md).

<!--Image references-->
[Node-to-Node]: ./media/service-fabric-cluster-security/node-to-node.png
[Client-to-Node]: ./media/service-fabric-cluster-security/client-to-node.png

