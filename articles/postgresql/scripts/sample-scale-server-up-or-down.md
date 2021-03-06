---
title: "Azure CLI 스크립트 - PostgreSQL용 Azure Database 확장 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 메트릭을 쿼리한 후에 PostgreSQL 서버용 Azure Database를 다양한 성능 수준으로 확장합니다."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.translationtype: HT
ms.sourcegitcommit: cf381b43b174a104e5709ff7ce27d248a0dfdbea
ms.openlocfilehash: b847abb336cce5dd5516469dca58002d3ba265f0
ms.contentlocale: ko-kr
ms.lasthandoff: 08/23/2017

---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a>Azure CLI를 사용하여 단일 PostgreSQL 서버 모니터링 및 확장
이 샘플 CLI 스크립트는 메트릭을 쿼리한 후에 PostgreSQL 서버용 단일 Azure Database를 다양한 성능 수준으로 확장합니다. 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다. `az --version`을 실행하여 버전을 찾습니다. 설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요. 

## <a name="sample-script"></a>샘플 스크립트
이 샘플 스크립트에서 강조 표시된 줄을 변경하여 관리자 사용자 이름 및 암호를 사용자 지정합니다. az monitor 명령에 사용된 구독 ID를 사용자 고유의 구독 ID로 바꿉니다. [!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "PostgreSQL용 Azure Database를 만들고 크기를 조정합니다.")]

## <a name="clean-up-deployment"></a>배포 정리
스크립트 샘플을 실행한 후에 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거할 수 있습니다.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "리소스 그룹을 삭제합니다.")]

## <a name="script-explanation"></a>스크립트 설명
이 스크립트는 다음 명령을 사용합니다. 테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.

| **명령** | **참고 사항** |
|---|---|
| [az group create](/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az postgres server create](/cli/azure/postgres/server#create) | 데이터베이스를 호스팅하는 PostgreSQL 서버를 만듭니다. |
| [az monitor metrics list](/cli/azure/monitor/metrics#list) | 리소스에 대한 메트릭 값을 나열합니다. |
| [az group delete](/cli/azure/group#delete) | 모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다. |

## <a name="next-steps"></a>다음 단계
- Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](/cli/azure/overview)를 참조하세요.
- 추가 스크립트 시도: [PostgreSQL용 Azure 데이터베이스 대한 Azure CLI 샘플](../sample-scripts-azure-cli.md)
- 크기 조정에 대한 자세한 내용은 [서비스 계층](../concepts-service-tiers.md) 및 [Compute 단위 및 Storage 단위](../concepts-compute-unit-and-storage.md)를 참조하세요.

