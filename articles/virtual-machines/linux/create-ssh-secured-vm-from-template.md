---
title: "템플릿에서 Azure에 Linux VM 만들기 | Microsoft Docs"
description: "Azure CLI 2.0을 사용하여 Resource Manager 템플릿에서 Linux VM을 만드는 방법"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.translationtype: Human Translation
ms.sourcegitcommit: 9568210d4df6cfcf5b89ba8154a11ad9322fa9cc
ms.openlocfilehash: 908a8a0c82b2d21fb25c9b33dbd714570d1ac272
ms.contentlocale: ko-kr
ms.lasthandoff: 05/15/2017


---
# <a name="how-to-create-a-linux-virtual-machine-with-azure-resource-manager-templates"></a>Azure Resource Manager 템플릿을 사용하여 Linux 가상 컴퓨터를 만드는 방법
이 문서에서는 Azure Resource Manager 템플릿 및 Azure CLI 2.0을 사용하여 Linux VM(가상 컴퓨터)을 신속하게 배포하는 방법을 보여 줍니다. [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md)에서 이러한 단계를 수행할 수도 있습니다.


## <a name="templates-overview"></a>템플릿 개요
Azure Resource Manager 템플릿은 Azure 솔루션의 인프라와 구성을 정의하는 JSON 파일입니다. 템플릿을 사용하여 수명 주기 내내 솔루션을 반복적으로 배포하고 안심하고 일관된 상태로 리소스를 배포할 수 있습니다. 템플릿의 형식 및 템플릿을 생성하는 방법에 대해 자세히 알아보려면 [첫 번째 Azure Resource Manager 템플릿 만들기](../../azure-resource-manager/resource-manager-create-first-template.md)를 참조하세요. 리소스 유형의 JSON 구문을 보려면 [Azure Resource Manager 템플릿에서 리소스 정의](/azure/templates/)를 참조하세요.


## <a name="create-resource-group"></a>리소스 그룹 만들기
Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 가상 컴퓨터보다 먼저 리소스 그룹을 만들어야 합니다. 다음 예제에서는 *eastus* 지역에 *myResourceGroupVM*이라는 리소스 그룹을 만듭니다.

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>가상 컴퓨터 만들기
다음 예제에서는 [az group deployment create](/cli/azure/group/deployment#create)를 사용하여 [이 Azure Resource Manager 템플릿](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json)에서 VM을 만듭니다. *~/.ssh/id_rsa.pub*의 내용과 같은 고유한 SSH 공용 키의 값을 제공합니다. SSH 키 쌍을 만들어야 하는 경우 [Azure에서 Linux VM용 SSH 키 쌍을 만들고 사용하는 방법](mac-create-ssh-keys.md)을 참조하세요.

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

이 예제에서는 GitHub에 저장된 템플릿을 지정했습니다. 또한 템플릿을 다운로드하거나 만들고 동일한 `--template-file` 매개 변수로 로컬 경로를 지정할 수도 있습니다.

VM에 SSH하려면 [az network public-ip show](/cli/azure/network/public-ip#show)를 사용하여 공용 IP 주소를 가져옵니다.

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

그런 다음 정상적으로 VM에 SSH할 수 있습니다.

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a>다음 단계
이 예제에서는 기본 Linux VM을 만들었습니다. 응용 프로그램 프레임워크를 포함하거나 더 복잡한 환경을 만드는 더 많은 Resource Manager 템플릿은 [Azure 빠른 시작 템플릿 갤러리](https://azure.microsoft.com/documentation/templates/)를 찾아보세요.
