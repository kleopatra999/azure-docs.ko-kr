---
title: "Azure Storage 작업을 위한 도구 | Microsoft Docs"
description: "Azure 저장소 데이터를 보고 상호 작용할 수 있는 도구 목록입니다."
services: storage
documentationcenter: 
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: e4748642-98c4-437e-b0ed-4f9641c2e894
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: dineshmurthy
ms.translationtype: HT
ms.sourcegitcommit: bde1bc7e140f9eb7bb864c1c0a1387b9da5d4d22
ms.openlocfilehash: 620efda06d8225b21b6bb9b104b79061ebb6515c
ms.contentlocale: ko-kr
ms.lasthandoff: 07/21/2017

---
# <a name="azure-storage-client-tools"></a>Azure 저장소 클라이언트 도구
Azure 저장소의 사용자는 Azure 저장소 클라이언트 도구를 사용하여 데이터를 보기/상호 작용하려는 경우가 많습니다. 아래 표에는 이 작업을 수행할 수 있게 해 주는 여러 도구가 나와 있습니다. 해당 도구가 데이터 추상화를 열거 및/또는 액세스할 수 있는 기능을 제공하는 경우 각 블록에 “X” 표시를 합니다. 또한 도구가 무료인지 여부도 나와 있습니다. “평가판”은 무료 평가판이 있음을 나타내지만 정품은 무료가 아님을 나타냅니다. “Y/N”는 특정 버전은 무료로 제공되지만 다른 버전은 구매할 수 있는지를 나타냅니다.

사용 가능한 Azure 저장소 클라이언트 도구의 스냅숏만 제공합니다. 이러한 도구의 기능은 계속 개선 및 확장될 수 있습니다. 수정 사항이나 업데이트가 있는 경우 의견을 남겨주세요. 여기에 포함해야 할 도구가 있는 경우에도 알려주시면 추가해 드리겠습니다.

**Microsoft Azure 저장소 클라이언트 도구**

<table>
  <tr>
    <th rowspan="2">Azure 저장소 클라이언트 도구</th>
    <th rowspan="2">블록 Blob</th>
    <th rowspan="2">페이지 Blob</th>
    <th rowspan="2">Blob 추가</th>
    <th rowspan="2">테이블</th>
    <th rowspan="2">큐</th>
    <th rowspan="2">파일</th>
    <th rowspan="2">무료</th>
    <th colspan="4">플랫폼</th>
  </tr>
  <tr>
    <td>웹</td>
    <td>Windows</td>
    <td>OSX</td>
    <td>Linux</td>
  </tr>
  <tr>
    <td><a href="https://azure.microsoft.com/features/azure-portal/">Microsoft Azure Portal</a></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>Y</td>
    <td>X</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="http://storageexplorer.com/">Microsoft Azure Storage Explorer</a></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>Y</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
  </tr>
  <tr>
    <td><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio 서버 탐색기</a></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>Y</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</table>

**타사 Azure 저장소 클라이언트 도구**

다음의 타사 도구가 주장하는 기능이나 품질은 보장할 수 없으며 목록에 포함되었다고 해서 Microsoft가 보증한다는 것을 의미하지 않습니다.

<table>
  <tr>
    <th rowspan="2">Azure 저장소 클라이언트 도구</th>
    <th rowspan="2">블록 Blob</th>
    <th rowspan="2">페이지 Blob</th>
    <th rowspan="2">Blob 추가</th>
    <th rowspan="2">테이블</th>
    <th rowspan="2">큐</th>
    <th rowspan="2">파일</th>
    <th rowspan="2">무료</th>
    <th colspan="4">플랫폼</th>
  </tr>
  <tr>
    <td>웹</td>
    <td>Windows</td>
    <td>OSX</td>
    <td>Linux</td>
  </tr>
  <tr>
    <td><a href="http://www.cloudportam.com/">Cloud Portam</a></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>평가판</td>
    <td>X</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>평가판</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Azure Explorer</a></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td></td>
    <td>X</td>
    <td>Y</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="https://github.com/sebagomez/azurestorageexplorer">Azure 저장소 탐색기</a></td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>Y</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td></td>
    <td></td>
    <td>X</td>
    <td>Y/N</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>평가판</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>Y</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></td>
    <td>X</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>평가판</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="http://storageexplorer.codeplex.com/">Azure Web Storage Explorer</a></td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>Y</td>
    <td>X</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="https://zudio.co/">Zudio</a></td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>평가판</td>
    <td>X</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>

