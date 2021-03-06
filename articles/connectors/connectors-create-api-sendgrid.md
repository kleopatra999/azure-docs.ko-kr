---
title: SendGrid | Microsoft Docs
description: "Azure 앱 서비스로 논리 앱을 만듭니다. SendGrid 연결 공급자를 통해 전자 메일을 보내고 받는 사람 목록을 관리할 수 있습니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: bc4f1fc2-824c-4ed7-8de8-e82baff3b746
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.translationtype: Human Translation
ms.sourcegitcommit: c785ad8dbfa427d69501f5f142ef40a2d3530f9e
ms.openlocfilehash: 9ff0591741899d65b8274fb14ab3f3c8db9abe36
ms.contentlocale: ko-kr
ms.lasthandoff: 05/26/2017


---
# <a name="get-started-with-the-sendgrid-connector"></a>SendGrid 커넥터 시작
SendGrid 연결 공급자를 통해 전자 메일을 보내고 받는 사람 목록을 관리할 수 있습니다.

이제 논리 앱을 만들어 시작할 수 있습니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.

## <a name="create-a-connection-to-sendgrid"></a>SendGrid에 대한 연결 만들기
SendGrid로 논리 앱을 만들려면 먼저 **연결**을 만든 후에 다음 속성에 대한 세부 정보를 제공해야 합니다. 

| 속성 | 필수 | 설명 |
| --- | --- | --- |
| ApiKey |예 |SendGrid API 키 제공 |

> [!INCLUDE [Steps to create a connection to SendGrid](../../includes/connectors-create-api-sendgrid.md)]
> 


연결을 만든 후에 사용하여 작업을 실행하고 트리거에 대한 수신을 대기할 수 있습니다.

## <a name="connector-specific-details"></a>커넥터 관련 세부 정보

[커넥터 세부 정보](/connectors/sendgrid/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.

## <a name="more-connectors"></a>추가 커넥터
[API 목록](apis-list.md)으로 돌아갑니다.
