---
title: "Azure Resource Manager 코어 할당량 증가 요청 | Microsoft Docs"
description: "Azure Resource Manager 코어 할당량 증가 요청"
author: ganganarayanan
ms.author: gangan
ms.date: 1/18/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: ce37c848-ddd9-46ab-978e-6a1445728a3b
ms.translationtype: Human Translation
ms.sourcegitcommit: 2373cf227cbed4f6657e31088b11dca5223ce5fe
ms.openlocfilehash: cb6c5b3e86f126d4110d1cd29d8c9891e356e414
ms.contentlocale: ko-kr
ms.lasthandoff: 07/06/2017


---

# <a name="resource-manager-core-quota-increase-requests"></a>Resource Manager 코어 할당량 증가 요청

Resource Manager 코어 할당량은 지역 수준 및 SKU 제품군 수준에 적용됩니다.
[Azure 구독 및 서비스 제한](http://aka.ms/quotalimits) 페이지에서 할당량이 적용되는 방식에 대해 자세히 알아보세요.
SKU 제품군에 대해 알아보려면 [Virtual Machines 가격 책정](http://aka.ms/pricingcompute) 페이지에서 비용과 성능을 비교할 수 있습니다.

증가를 요청하려면 Azure Portal [https://portal.azure.com](https://portal.azure.com)에서 코어에 대한 할당량 지원 사례를 만듭니다.

> [!NOTE]
> Azure Portal에서 [지원 요청을 만드는](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) 방법 알아보기

1. 새 지원 요청 페이지에서 문제 유형은 "할당량"으로 할당량 유형은 "코어"로 선택합니다.

    ![할당량 기본 사항 블레이드](./media/resource-manager-core-quotas-request/Basics-blade.png)

2. 배포 모델을 "Resource Manager"로 선택하고 위치를 선택합니다.

    ![할당량 문제 블레이드](./media/resource-manager-core-quotas-request/Problem-step.png)

3. 증가가 필요한 SKU 제품군을 선택합니다.

    ![SKU 시리즈 선택됨](./media/resource-manager-core-quotas-request/SKU-selected.png)

4. 구독에 대한 새 한도를 입력합니다.

    ![SKU 새 할당량 요청](./media/resource-manager-core-quotas-request/SKU-new-quota.png)

- 줄을 제거하려면 SKU 제품군 드롭다운에서 SKU 선택을 해제하거나 삭제 "x" 아이콘을 클릭합니다.
각 SKU 제품군에 대해 원하는 할당량을 입력한 다음 문제 단계 페이지에서 "다음"을 클릭하여 지원 요청 만들기를 계속합니다.

