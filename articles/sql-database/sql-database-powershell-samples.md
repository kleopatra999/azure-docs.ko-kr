---
title: "SQL Database에 대한 Azure PowerShell 스크립트 예제 | Microsoft Docs"
description: "Azure SQL Database 서버, 탄력적 풀, 데이터베이스 및 방화벽을 만들고 관리하는 데 유용한 Azure PowerShell 스크립트 예제입니다."
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: overview-samples
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.translationtype: HT
ms.sourcegitcommit: 99523f27fe43f07081bd43f5d563e554bda4426f
ms.openlocfilehash: 5a5f77b9adafe32e8559d0b3396febca4b191de3
ms.contentlocale: ko-kr
ms.lasthandoff: 08/05/2017

---

# <a name="azure-powershell-samples-for-azure-sql-database"></a>Azure SQL Database에 대한 Azure PowerShell 샘플

다음 표에는 Azure SQL Database의 Azure PowerShell 샘플 스크립트에 대한 링크가 나와 있습니다.

| |  |
|---|---|
|**단일 데이터베이스 및 탄력적 풀 만들기**||
| [단일 데이터베이스 만들기 및 방화벽 규칙 구성](scripts/sql-database-create-and-configure-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 이 PowerShell 스크립트는 단일 Azure SQL Database를 만들고 서버 수준 방화벽 규칙을 구성합니다. |
| [탄력적 풀 만들기 및 풀된 데이터베이스 이동](scripts/sql-database-move-database-between-pools-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 이 PowerShell 스크립트는 Azure SQL Database 탄력적 풀을 만들고 풀된 데이터베이스를 이동한 후 성능 수준을 변경합니다.|
|**지역에서 복제 및 장애 조치(failover) 구성**||
| [활성 지역 복제를 사용하여 단일 데이터베이스 구성 및 장애 조치(failover)](scripts/sql-database-setup-geodr-and-failover-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| 이 PowerShell 스크립트는 단일 Azure SQL Database에 대해 활성 지역 복제를 구성하고 보조 복제본으로 장애 조치(failover)합니다. |
| [활성 지역 복제를 사용하여 풀된 데이터베이스 구성 및 장애 조치(failover)](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| 이 PowerShell 스크립트는 SQL 탄력적 풀의 단일 Azure SQL Database에 대해 활성 지역 복제를 구성하고 보조 복제본으로 장애 조치(failover)합니다. |
| [단일 데이터베이스에 대한 장애 조치(failover) 그룹 구성 및 장애 조치(failover)(미리 보기)](scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 이 PowerShell 스크립트는 Azure SQL Database 서버 인스턴스의 장애 조치(failover) 그룹을 구성하고, 장애 조치(failover) 그룹에 데이터베이스를 추가하고, 보조 서버로 장애 조치(failover)합니다. |
|**단일 데이터베이스 및 탄력적 풀 크기 조정**||
| [단일 데이터베이스 크기 조정](scripts/sql-database-monitor-and-scale-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 이 PowerShell 스크립트는 Azure SQL Database의 성능 메트릭을 모니터링하고, 더 높은 성능 수준으로 확장하고, 성능 메트릭 중 하나에 경고 규칙을 만듭니다. |
| [탄력적 풀 크기 조정](scripts/sql-database-monitor-and-scale-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 이 PowerShell 스크립트는 Azure SQL Database 탄력적 풀의 성능 메트릭을 모니터링하고, 더 높은 성능 수준으로 확장하고, 성능 메트릭 중 하나에 경고 규칙을 만듭니다.  |
| **감사 및 위협 감지** |
| [감사 및 위협 감지 구성](scripts/sql-database-auditing-and-threat-detection-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| 이 PowerShell 스크립트는 Azure SQL Database에 대한 감사 및 위협 감지 정책을 구성합니다. |
| **데이터베이스 복원, 복사 및 가져오기**||
| [데이터베이스 복원](scripts/sql-database-restore-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| 이 PowerShell 스크립트는 지역 중복 백업에서 Azure SQL Database를 복원하고 삭제된 Azure SQL Database를 최신 백업으로 복원합니다. |
| [새 서버에 데이터베이스 복사](scripts/sql-database-copy-database-to-new-server-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| 이 PowerShell 스크립트는 새 Azure SQL Server에 기존 Azure SQL Database의 복사본을 만듭니다. |
| [bacpac 파일에서 데이터베이스 가져오기](scripts/sql-database-import-from-bacpac-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| 이 PowerShell 스크립트는 bacpac 파일에서 Azure SQL Server로 데이터베이스를 가져옵니다. |
| **데이터베이스 간 데이터 동기화**||
| [SQL Database 간 데이터 동기화](scripts/sql-database-sync-data-between-sql-databases.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 이 PowerShell 스크립트는 여러 Azure SQL Database 간에 동기화를 수행하도록 데이터 동기화를 구성합니다. |
| [SQL Database 및 SQL Server 온-프레미스 간의 데이터 동기화](scripts/sql-database-sync-data-between-azure-onprem.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 이 PowerShell 스크립트는 Azure SQL Database와 SQL Server 온-프레미스 데이터베이스 간에 동기화를 수행하도록 데이터 동기화를 구성합니다. |
|||
|||

