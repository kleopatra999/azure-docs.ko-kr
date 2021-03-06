---
title: "Azure PowerShell 스크립트 샘플 - Service Fabric 응용 프로그램 업그레이드 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - Service Fabric 응용 프로그램 업그레이드"
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: sample
ms.date: 08/23/2017
ms.author: ryanwi
ms.custom: mvc
ms.translationtype: HT
ms.sourcegitcommit: 25e4506cc2331ee016b8b365c2e1677424cf4992
ms.openlocfilehash: 43c1c0d38d12a36c39a3962a3399d9c05937e8b1
ms.contentlocale: ko-kr
ms.lasthandoff: 08/24/2017

---

# <a name="upgrade-a-service-fabric-application"></a>Service Fabric 응용 프로그램 업그레이드

이 샘플 스크립트는 실행 중인 Service Fabric 응용 프로그램 인스턴스를 버전 1.3.0으로 업그레이드합니다. 이 스크립트는 클러스터 이미지 저장소에 새 응용 프로그램 패키지를 복사하고, 응용 프로그램 유형을 등록하고, 모니터링되는 업그레이드를 시작하고, 업그레이드가 완료되거나 롤백될 때까지 업그레이드 상태를 계속 확인합니다. 필요에 따라 매개 변수를 사용자 지정합니다. 

필요한 경우 [Service Fabric SDK](../service-fabric-get-started.md)를 사용하여 Service Fabric PowerShell 모듈을 설치합니다. 

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "응용 프로그램 업그레이드")]

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 다음 명령을 사용합니다. 테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.

| 명령 | 참고 |
|---|---|
| [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | Service Fabric 클러스터의 모든 응용 프로그램 또는 특정 응용 프로그램을 가져옵니다.  |
| [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | Service Fabric 응용 프로그램 업그레이드의 상태를 가져옵니다. |
| [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | Service Fabric 클러스터에 등록된 Service Fabric 응용 프로그램 유형을 가져옵니다. |
| [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | Service Fabric 응용 프로그램 유형을 등록 취소합니다.  |
| [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | Service Fabric 응용 프로그램 패키지를 이미지 저장소에 복사합니다.  |
| [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | Service Fabric 응용 프로그램 유형을 등록합니다. |
| [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | Service Fabric 응용 프로그램을 지정된 응용 프로그램 유형 버전으로 업그레이드합니다. |


## <a name="next-steps"></a>다음 단계

Service Fabric PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/service-fabric/?view=azureservicefabricps)를 참조하세요.

Azure Service Fabric에 대한 추가 PowerShell 샘플은 [Azure PowerShell 샘플](../service-fabric-powershell-samples.md)에서 확인할 수 있습니다.

