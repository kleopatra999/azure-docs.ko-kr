---
title: "Azure API Management에서 역할 기반 액세스 제어를 사용하는 방법 | Microsoft Docs"
description: "Azure API Management에서 기본 제공 역할을 사용하고 사용자 지정 역할을 만드는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: apimpm
ms.translationtype: HT
ms.sourcegitcommit: 07e5e15f4f4c4281a93c8c3267c0225b1d79af45
ms.openlocfilehash: a3a874b8fc4e4dcfd7b194149f677127d9f9a200
ms.contentlocale: ko-kr
ms.lasthandoff: 08/31/2017

---

# <a name="how-to-use-role-based-access-control-in-azure-api-management"></a>Azure API Management에서 역할 기반 액세스 제어를 사용하는 방법
Azure API Management는 Azure 역할 기반 액세스 제어(RBAC)를 사용하여 API Management 서비스 및 엔터티(예: API, 정책)에 대한 세분화된 액세스 관리를 가능하게 합니다. 이 문서에서는 API Management에서 기본 제공 및 사용자 지정 역할에 대한 개요를 제공합니다. Azure Portal에서 액세스 관리에 대한 자세한 내용을 보려면 [Azure Portal에서 액세스 관리 시작](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)을 참조하세요.

## <a name="built-in-roles"></a>기본 제공 역할
API Management는 현재 3가지 기본 제공 역할을 제공하며 곧 2가지 역할을 추가할 예정입니다. 이러한 역할은 구독, 리소스 그룹 및 개별 API Management 인스턴스를 포함하여 서로 다른 범위에서 할당될 수 있습니다. 예를 들어 "Azure API Management 서비스 독자" 역할이 리소스 그룹 수준의 사용자에게 할당된 경우 사용자는 리소스 그룹 내의 모든 API Management 인스턴스에 대한 읽기 권한을 가지게 됩니다. 

다음 테이블은 기본 제공 역할을 간략하게 설명합니다. Azure Portal 또는 Azure [PowerShell](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-powershell), Azure [명령줄 인터페이스](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-azure-cli) 및 [REST API](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-rest)를 비롯한 다른 도구를 사용하여 이러한 역할을 할당할 수 있습니다. 기본 제공 역할을 할당하는 방법에 대한 자세한 내용은 [역할 할당을 사용하여 Azure 구독 리소스에 대한 액세스 관리](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)를 참조하세요.

| 역할          | 읽기 액세스<sup>[1]</sup> | 쓰기 액세스<sup>[2]</sup> | 서비스 만들기, 삭제, 크기 조정, VPN 및 사용자 지정 도메인 구성 | 기존 게시자 포털에 대한 액세스 | 설명
| ------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| API Management 서비스 참가자 | ✓ | ✓ | ✓ | ✓ | 슈퍼 사용자. API Management 서비스 및 엔터티(예: API, 정책)에 대한 전체 CRUD 액세스 권한을 보유합니다. 기존 게시자 포털에 대한 액세스 권한을 보유합니다. |
| Azure API Management 서비스 독자 | ✓ | | || API Management 서비스 및 엔터티에 대한 읽기 전용 액세스 권한을 보유합니다. |
| Azure API Management 서비스 연산자 | ✓ | | ✓ | | 엔터티가 아닌 API Management 서비스를 관리할 수 있습니다.|
| Azure API Management 서비스 편집기<sup>*</sup> | ✓ | ✓ | |  | API Management 엔터티는 관리할 수 있지만 서비스는 관리할 수 없습니다.|
| Azure API Management 콘텐츠 관리자<sup>*</sup> | ✓ | | | ✓ | 개발자 포털을 관리할 수 있습니다. 서비스 및 엔터티에 대한 읽기 전용 액세스.|

<sup>[1] API Management 서비스 및 엔터티(예: API, 정책)에 대한 읽기 권한</sup>

<sup>[2] 다음 작업을 제외한 API Management 서비스 및 엔터티에 대한 쓰기 권한: 1) 인스턴스 생성, 삭제 및 확장 2) VPN 구성 3) 사용자 지정 도메인 이름 설정</sup>

<sup>\* 서비스 편집자 역할은 모든 관리 UI를 기존 게시자 포털에서 Azure Portal로 마이그레이션한 후에 사용할 수 있습니다. 개발자 포털 관리와 관련된 기능만 포함하도록 게시자 포털을 리팩토링한 후에 콘텐츠 관리자 역할을 사용할 수 있습니다.</sup>  


## <a name="custom-roles"></a>사용자 지정 역할
기본 제공 역할이 사용자의 특정 요구 사항을 충족시키지 못하면 API Management 엔터티에 대한 보다 세분화된 액세스 관리를 제공하는 사용자 지정 역할을 작성할 수 있습니다. 예를 들어 API Management 서비스에 대해서는 읽기 전용 액세스 권한을 보유하지만 하나의 특정 API에 대해서는 쓰기 권한만 보유하는 사용자 지정 역할을 만들 수 있습니다. 사용자 지정 역할에 대한 자세한 내용은 [Azure RBAC에서 사용자 지정 역할](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles)을 참조하세요. 

사용자 지정 역할을 만들 때는 기본 제공 역할 중 하나로 시작하는 것이 쉽습니다. 속성을 편집하여 Actions, NotActions 또는 AssignableScopes를 추가한 다음 변경 사항을 새 역할로 저장합니다. 다음 예제는 "Azure API Management 서비스 독자" 역할로 시작하고 "Calculator API Editor"라는 사용자 지정 역할을 만듭니다. 사용자 지정 역할은 특정 API에만 할당될 수 있으므로 해당 API에 대한 액세스 권한만 보유합니다. 

```
$role = Get-AzureRmRoleDefinition "API Management Service Reader Role"
$role.Id = $null
$role.Name = 'Calculator API Contributor'
$role.Description = 'Has read access to Contoso APIM instance and write access to the Calculator API.'
$role.Actions.Add('Microsoft.ApiManagement/service/apis/write')
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add('/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>')
New-AzureRmRoleDefinition -Role $role
New-AzureRmRoleAssignment -ObjectId <object ID of the user account> -RoleDefinitionName 'Calculator API Contributor' -Scope '/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>'
```

## <a name="watch-a-video-overview"></a>비디오 개요 보기

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Role-Based-Access-Control-in-API-Management/player]
> 
> 

## <a name="next-steps"></a>다음 단계

* Azure의 역할 기반 액세스 제어에 대한 자세한 정보
  * [Azure 포털에서 액세스 관리 시작](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [역할 할당을 사용하여 Azure 구독 리소스에 대한 액세스 관리](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Azure RBAC에서 사용자 지정 역할](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles)

