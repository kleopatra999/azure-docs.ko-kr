---
title: "Azure CLI를 사용하여 리소스 관리 | Microsoft Docs"
description: "Azure 명령줄 인터페이스 (CLI)를 사용하여 Azure 리소스 및 그룹 관리"
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.translationtype: Human Translation
ms.sourcegitcommit: 5bbeb9d4516c2b1be4f5e076a7f63c35e4176b36
ms.openlocfilehash: 3ad4e68b90979fd7f9d3ddf5278e65e19cb07152
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017


---
# <a name="use-the-azure-cli-to-manage-azure-resources-and-resource-groups"></a>Azure 리소스 및 리소스 그룹 관리를 위해 Azure CLI 사용
> [!div class="op_single_selector"]
> * [포털](resource-group-portal.md) 
> * [Azure CLI](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [REST API](resource-manager-rest-api.md)
> 
> 

Azure 명령줄 인터페이스 (Azure CLI)는 리소스 관리자를 사용하여 리소스를 배포하고 관리하는 데 사용할 수 있는 몇 가지 도구 중 하나입니다. 이 문서에서는 리소스 관리자 모드에서 Azure CLI를 사용하여 Azure 리소스 및 리소스 그룹을 관리하는 일반적인 방법을 소개합니다. 리소스를 배포하기 위해 CLI를 사용하는 방법에 대한 정보는 [Resource Manager 템플릿 및 Azure CLI를 사용하여 리소스 배포](resource-group-template-deploy-cli.md)를 참조하세요. Azure 리소스 및 Resource Manager에 대한 기본 지식은 [Azure Resource Manager 개요](resource-group-overview.md)를 참조하세요.

> [!NOTE]
> Azure CLI를 사용하여 Azure 리소스를 관리하려면 `azure login` 명령을 사용하여 [Azure CLI를 설치](../cli-install-nodejs.md)하고 [Azure에 로그인](../xplat-cli-connect.md)합니다. CLI가 리소스 관리자 모드에 있는지 확인합니다.(`azure config mode arm`를 실행함) 이러한 작업이 완료되면 사용할 준비가 된 것입니다.
> 
> 

## <a name="get-resource-groups-and-resources"></a>리소스 그룹 및 리소스 가져오기
### <a name="resource-groups"></a>리소스 그룹
구독 및 해당 위치에서 모든 리소스 그룹 목록을 가져오려면 이 명령을 실행합니다.

    azure group list


### <a name="resources"></a>리소스
 이름이 *testRG*인 리소스 등, 그룹의 모든 리소스를 나열하려면 다음 명령을 사용합니다.

    azure resource list testRG

이름이 *MyUbuntuVM*인 VM 등, 그룹 내의 개별 리소스를 보려면 다음과 같은 명령을 사용합니다.

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

**Microsoft.Compute/virtualMachines** 매개 변수에 유의하세요. 이 매개 변수는 정보를 요청하는 대상 리소스의 유형을 나타냅니다.

> [!NOTE]
> **list** 명령이 아닌 **azure resource** 명령을 사용할 경우 **-o** 매개 변수를 사용하여 리소스의 API 버전을 지정해야 합니다. API 버전에 관해 확실하지 않은 경우 템플릿 파일을 참조하여 리소스의 apiVersion 필드를 찾아봅니다. Resource Manager의 API 버전에 대한 자세한 내용은 [리소스 공급자 및 형식](resource-manager-supported-services.md)을 참조하세요.
> 
> 

`--json` 매개 변수는 보통 리소스 세부 정보를 볼 때 유용하게 사용됩니다. 일부 값이 중첩된 구조이거나 컬렉션이기 때문에 이 매개 변수를 사용하면 출력을 읽기가 훨씬 수월합니다. 다음 예제에서는 **show** 명령의 결과를 JSON 문서로 반환하는 방법을 보여 줍니다.

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> 원하는 경우 &gt; 문자를 사용하여 파일에 출력되도록 하여 JSON 데이터를 파일에 저장합니다. 예:
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a>태그
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a>리소스 관리
리소스 그룹에 저장소 계정과 같은 리소스를 추가하려면 다음과 비슷한 명령을 실행합니다.

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

**-o** 매개 변수를 사용하여 리소스의 API 버전을 지정하는 외에도 **-p** 매개 변수를 사용하여 JSON 형식 문자열을 필수 또는 추가적인 속성과 함께 전달합니다.

가상 컴퓨터 리소스와 같은 기존 리소스를 삭제하려면 다음과 같은 명령을 사용합니다.

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

다른 리소스 그룹 또는 구독에 기존 리소스를 이동하려면 **azure resource move** 명령을 사용합니다. 다음 예제에서는 Redis Cache를 새 리소스 그룹으로 이동하는 방법을 보여 줍니다. **-i** 매개 변수에서 이동할 리소스 ID를 쉼표로 구분한 목록을 제공합니다.

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-to-resources"></a>리소스에 대한 액세스 제어
Azure CLI를 사용하여 Azure 리소스에 대한 액세스를 제어하는 정책을 만들고 관리할 수 있습니다. 정책 정의 및 리소스에 정책 할당에 관한 배경 지식은 [정책을 사용하여 리소스 및 컨트롤 액세스 관리](resource-manager-policy.md)를 참조하세요.

예를 들어, 위치가 미국 서부 또는 미국 북중부가 아닌 모든 요청을 거부하도록 다음 정책을 정의하고 정책 정의 파일인 policy.json에 저장합니다.

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

그런 다음 **policy definition create**명령을 실행합니다.

    azure policy definition create MyPolicy -p c:\temp\policy.json

이 명령은 다음과 유사한 출력을 표시합니다.

    + Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy

    data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny

 정책을 원하는 범위에 할당하려면 이전 명령에서 반환된 **PolicyDefinitionId**를 사용합니다. 다음 예제에서 이 범위는 해당 구독이지만 리소스 그룹이나 개별 리소스에 범위를 지정할 수 있습니다.

    azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/

**policy definition show**, **policy definition set** 및 **policy definition delete** 명령을 사용하여 정책 정의를 가져오거나, 변경하거나 또는 없앨 수 있습니다.

마찬가지로, **policy assignment show**, **policy assignment set** 및 **policy assignment delete** 명령을 사용하여 정책 할당을 가져오거나, 변경하거나 또는 없앨 수 있습니다.

## <a name="export-a-resource-group-as-a-template"></a>리소스 그룹을 템플릿으로 내보내기
기존 리소스 그룹에 대해 해당 리스소 그룹의 리소스 관리자 템플릿을 볼 수 있습니다. 템플릿을 내보내면 다음과 같은 두 가지 이점이 있습니다.

1. 모든 인프라가 템플릿에 정의되어 있기 때문에 향후 솔루션 배포를 간단하게 자동화할 수 있습니다.
2. 솔루션을 나타내는 JSON을 살펴보면서 템플릿 구문에 익숙해질 수 있습니다.

Azure CLI를 사용하여 리소스 그룹의 현재 상태를 나타내는 템플릿을 내보내거나 특정 배포에 사용된 템플릿을 다운로드할 수 있습니다.

* **리소스 그룹에 대한 템플릿 내보내기** - 리소스 그룹을 변경했고 현재 상태의 JSON 표현을 검색해야 하는 경우 유용합니다. 그러나 생성된 템플릿에는 최소한의 매개 변수만 포함되고 변수는 포함되지 않습니다. 템플릿의 값은 대부분 하드 코드됩니다. 생성된 템플릿을 배포하기 전에, 다양한 환경에 맞게 배포를 사용자 지정할 수 있도록 더 많은 값을 매개 변수로 변환할 수 있습니다.
  
    리소스 그룹에 대한 템플릿을 로컬 디렉터리로 내보내려면 다음 예제처럼 `azure group export` 명령을 실행합니다. (운영 체제 환경에 맞게 적합한 로컬 디렉터리로 대체)
  
        azure group export testRG ~/azure/templates/
* **특정 배포에 대한 템플릿 다운로드** -- 리소스를 배포하는 데 사용된 실제 템플릿을 살펴보아야 하는 경우에 유용합니다. 이 템플릿에는 원래 배포에 대해 정의된 모든 매개 변수와 변수가 포함됩니다. 그러나 조직 내 다른 사람이 템플릿에 정의된 범위를 넘어서 리소스 그룹을 변경할 경우 이 템플릿은 리소스 그룹의 현재 상태를 나타내지 않습니다.
  
    특정 배포에 사용한 템플릿을 로컬 디렉터리에 다운로드하려면 `azure group deployment template download` 명령을 실행합니다. 예:
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> 템플릿 내보내기는 미리 보기 버전이며, 템플릿 내보내기를 지원하지 않는 리소스 유형도 있습니다. 템플릿 내보내기를 시도할 때 일부 리소스를 내보내지 못했다는 오류가 표시될 수 있습니다. 필요한 경우 템플릿을 다운로드한 후 템플릿에서 이러한 리소스를 수동으로 정의합니다.
> 
> 

## <a name="next-steps"></a>다음 단계
* Azure CLI를 사용하여 배포 작업의 자세한 내용을 보고 배포 오류의 문제를 해결하려면 [배포 작업 보기](resource-manager-deployment-operations.md)를 참조하세요.
* CLI를 사용하여 리소스에 액세스하도록 응용 프로그램이나 스크립트를 설정하려면 [Azure CLI를 사용하여 리소스에 액세스하는 서비스 주체 만들기](resource-group-authenticate-service-principal-cli.md)를 참조하세요.
* 엔터프라이즈에서 리소스 관리자를 사용하여 구독을 효과적으로 관리할 수 있는 방법에 대한 지침은 [Azure 엔터프라이즈 스캐폴드 - 규범적 구독 거버넌스](resource-manager-subscription-governance.md)를 참조하세요.


