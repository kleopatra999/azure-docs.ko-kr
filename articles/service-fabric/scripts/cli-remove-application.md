---
title: "Azure Service Fabric CLI 스크립트 제거 샘플"
description: "Azure Service Fabric CLI를 사용하여 Azure Service Fabric 클러스터에 응용 프로그램 제거"
services: service-fabric
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: sample
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.translationtype: HT
ms.sourcegitcommit: 25e4506cc2331ee016b8b365c2e1677424cf4992
ms.openlocfilehash: 6ea52da6698647bb21d8f4c9a47a73bd5eef2a29
ms.contentlocale: ko-kr
ms.lasthandoff: 08/24/2017

---

# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Service Fabric 클러스터에서 응용 프로그램 제거

이 샘플 스크립트는 실행 중인 Service Fabric 응용 프로그램 인스턴스를 삭제하고, 클러스터에서 응용 프로그램 유형 및 버전의 등록을 취소합니다.  응용 프로그램 인스턴스를 삭제하면 해당 응용 프로그램과 연결된 실행 중인 모든 서비스 인스턴스도 삭제됩니다. 다음으로 응용 프로그램 파일을 이미지 저장소에서 삭제합니다. 

필요한 경우 [Service Fabric CLI](../service-fabric-cli.md)를 설치합니다.

## <a name="sample-script"></a>샘플 스크립트

[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "클러스터에서 응용 프로그램 제거")]

## <a name="next-steps"></a>다음 단계

자세한 내용은 [Service Fabric CLI 설명서](../service-fabric-cli.md)를 참조하세요.

Azure Service Fabric에 대한 추가 Service Fabric CLI 샘플은 [Service Fabric CLI 샘플](../samples-cli.md)에서 확인할 수 있습니다.

