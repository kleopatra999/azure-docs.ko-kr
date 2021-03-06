---
title: "레거시 Azure Virtual Network 게이트웨이 SKU | Microsoft Docs"
description: "이전 가상 네트워크 게이트웨이 SKU입니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.translationtype: HT
ms.sourcegitcommit: 1e6fb68d239ee3a66899f520a91702419461c02b
ms.openlocfilehash: 3b2126b1ecd1613950bbf311ae08fafd4af0d51f
ms.contentlocale: ko-kr
ms.lasthandoff: 08/16/2017

---
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a>가상 네트워크 게이트웨이 SKU(레거시 SKU) 사용

이 문서에는 레거시(이전) 가상 네트워크 게이트웨이 SKU에 대한 정보가 포함되어 있습니다. 레거시 SKU는 이미 작성된 VPN Gateway의 두 배포 모델에서 모두 계속 작동합니다. 클래식 VPN Gateway는 레거시 SKU를 계속 사용합니다(기존 게이트웨이와 새 게이트웨이 둘 다를 위해). 새 Resource Manager VPN Gateway를 만들 때는 새 게이트웨이 SKU를 사용합니다. 새 SKU에 대한 자세한 내용은 [VPN Gateway 정보](vpn-gateway-about-vpngateways.md)를 참조하세요.

## <a name="gwsku"></a>게이트웨이 SKU

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <a name="agg"></a>SKU 기준으로 예상된 총 처리량

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <a name="config"></a>SKU와 VPN 형식별 지원되는 구성

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <a name="resize"></a>게이트웨이 크기 조정(게이트웨이 SKU 변경)

동일한 SKU 제품군 내에서 게이트웨이 SKU 크기를 조정할 수 있습니다. 예를 들어 Standard SKU는 HighPerformance SKU로 크기를 조정할 수 있습니다. 이전 SKU와 새 SKU 제품군 간에 VPN Gateway의 크기를 조정할 수는 없습니다. 예를 들어 Standard SKU에서 VpnGw2 SKU로 크기를 조정할 수는 없습니다. 

클래식 배포 모델의 게이트웨이 SKU 크기를 조정하려면 다음 명령을 사용합니다.

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

Resource Manager 배포 모델의 게이트웨이 SKU 크기를 조정하려면 다음 명령을 사용합니다.

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="migrate"></a>새 게이트웨이 SKU로 마이그레이션

Resource Manager 배포 모델을 사용하는 경우 새 게이트웨이 SKU로 마이그레이션할 수 있습니다. 클래식 배포 모델을 사용하는 경우에는 새 SKU로 마이그레이션할 수 없으며 대신 레거시 SKU를 계속 사용해야 합니다.

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a>다음 단계

새 게이트웨이 SKU에 대한 자세한 내용은 [게이트웨이 SKU](vpn-gateway-about-vpngateways.md#gwsku)를 참조하세요.

구성 설정에 대한 자세한 내용은 [VPN Gateway 구성 설정 정보](vpn-gateway-about-vpn-gateway-settings.md)를 참조하세요.
