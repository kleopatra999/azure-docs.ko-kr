---
title: "Azure CLI 스크립트 샘플 - ACS DC/OS 클러스터 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - ACS DC/OS 클러스터 만들기"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: nepeters
ms.translationtype: HT
ms.sourcegitcommit: bfd49ea68c597b109a2c6823b7a8115608fa26c3
ms.openlocfilehash: ff90aee308a993ae0d36288191d1496affacce2a
ms.contentlocale: ko-kr
ms.lasthandoff: 07/25/2017

---

# <a name="create-an-azure-container-service-dcos-cluster"></a>Azure Container Service DC/OS 클러스터 만들기

이 샘플에서는 DC/OS를 실행하는 Azure Container Service 클러스터를 만듭니다.

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a>배포 정리 

다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 다음 명령을 사용하여 배포합니다. 테이블에 있는 각 항목은 명령에 해당하는 문서에 연결됩니다.

| 명령 | 참고 사항 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az acs create](https://docs.microsoft.com/cli/azure/acs#create) | ACS 클러스터를 만듭니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.

추가 Azure Container Service CLI 스크립트 샘플은 [Azure Container Service 설명서](../cli-samples.md)에서 확인할 수 있습니다.
