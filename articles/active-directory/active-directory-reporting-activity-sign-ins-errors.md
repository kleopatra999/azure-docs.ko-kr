---
title: "Azure Active Directory 포털의 로그인 활동 보고서 오류 코드 | Microsoft Docs"
description: "로그인 활동 보고서 오류 코드에 대한 참조입니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.translationtype: HT
ms.sourcegitcommit: bde1bc7e140f9eb7bb864c1c0a1387b9da5d4d22
ms.openlocfilehash: 2a1b7b87df2cd8fa2e98f217480b46f5f6334297
ms.contentlocale: ko-kr
ms.lasthandoff: 07/21/2017

---
# <a name="sign-in-activity-report-error-codes-in-the-azure-active-directory-portal"></a>Azure Active Directory 포털의 로그인 활동 보고서 오류 코드

사용자 로그인 보고서에서 제공되는 정보를 사용하면 다음과 같은 질문에 대한 대답을 찾을 수 있습니다.

- Azure Active Directory를 사용하여 로그인한 사람은?
- 서명된 앱은?
- 실패한 로그인은? 그리고 실패한 경우 이유는?

이 항목에서는 오류 코드와 관련 설명이 나와 있습니다. 

## <a name="how-can-i-display-failed-sign-ins"></a>실패한 로그인을 표시하려면 어떻게 해야 합니까? 

모든 로그인 활동 데이터에 대한 첫 번째 진입점은 **Azure Active**의 **활동** 섹션에 있는 **[로그인](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/SignIns)**입니다.


![로그인 활동](./media/active-directory-reporting-activity-sign-ins-errors/61.png "로그인 활동")


로그인 보고서에서 **실패**를 **로그인 상태**로 선택하여 실패한 로그인을 모두 표시할 수 있습니다.


![로그인 활동](./media/active-directory-reporting-activity-sign-ins-errors/06.png "로그인 활동")

표시된 목록에서 항목을 클릭하면 **활동 세부 정보: 로그인**  블레이드가 열립니다. 이 보기에서는 **로그인 오류 코드** 및 **실패 이유**를 포함하여 Azure Active Directory에서 로그인에 대해 추적하는 모든 세부 정보를 제공합니다.

![로그인 활동](./media/active-directory-reporting-activity-sign-ins-errors/05.png "로그인 활동")


Azure Portal을 사용하여 로그인 데이터에 액세스하는 대신 [보고 API](active-directory-reporting-api-getting-started-azure-portal.md)를 사용할 수도 있습니다.


다음 섹션에서는 가능한 모든 오류 및 관련 설명에 대한 전체 개요를 제공합니다. 

## <a name="error-codes"></a>오류 코드

| 오류| 설명 |
| --- | --- |
| 50001| X라는 서비스 주체가 Y라는 테넌트에 없습니다. 테넌트의 관리자가 응용 프로그램을 설치하지 않은 경우에 발생할 수 있습니다. 또는 리소스 보안 주체가 디렉터리에 없거나 잘못되었습니다.|
| 50008| 토큰에서 SAML 어설션이 누락되었거나 잘못 구성되었습니다.|
| 50011| 회신 주소가 누락되었거나 잘못 구성되었거나 응용 프로그램에 대해 구성된 회신 주소와 일치하지 않습니다.|
| 50053| 잘못된 사용자 ID 또는 암호로 로그인을 너무 많이 시도하여 계정이 잠겨 있습니다.|
| 50054| 이전 암호가 인증에 사용되었습니다.|
| 50055| 잘못된 암호입니다. 만료된 암호를 입력했습니다.|
| 50057| 사용자 계정을 사용할 수 없습니다.|
| 50058| 제공된 자격 증명에서 사용자의 ID에 대한 정보가 없거나, 테넌트에서 사용자를 찾을 수 없거나, 자동 로그인 요청을 보냈지만 사용자가 로그인되지 않았거나 서비스에서 사용자를 인증하지 못했습니다.|
| 50074| 강력한 인증(2단계)이 필요합니다.|
| 50079| 사용자는 2단계 인증에 등록해야 합니다.|
| 50126| 잘못된 사용자 이름 또는 암호이거나 잘못된 온-프레미스 사용자 이름 또는 암호입니다.|
| 50131| 다양한 조건부 액세스 오류에 사용됩니다. 예: Windows 장치 상태가 잘못되었습니다. 의심스러운 활동, 액세스 정책 및 보안 정책 결정으로 인해 요청이 차단되었습니다.|
| 50133| 만료 또는 최근 암호 변경으로 인해 세션이 잘못되었습니다.|
| 50144| 사용자의 Active Directory 암호가 만료되었습니다.|
| 65001| Y 응용 프로그램에 대한 액세스 권한이 X 응용 프로그램에 없거나 권한이 취소되었습니다. 또는 사용자 또는 관리자가 X ID로 응용 프로그램을 사용하는 데 동의하지 않았습니다. 이 사용자 및 리소스에 대한 대화형 권한 부여 요청을 보내세요. 또는 사용자 또는 관리자가 X ID로 응용 프로그램을 사용하는 데 동의하지 않았습니다. Z 리소스에 대한 Y 앱을 대신하여 테넌트 관리자에게 권한 부여 요청을 보내세요.|
| 65005| 응용 프로그램 필수 리소스 액세스 목록에 리소스에서 검색 가능한 응용 프로그램이 없거나, 클라이언트 응용 프로그램에서 필수 리소스 액세스 목록에 지정되지 않은 리소스에 대한 액세스를 요청했거나, Graph 서비스에서 잘못된 요청 또는 찾을 수 없는 리소스를 반환했습니다.|
| 70001| X라는 응용 프로그램이 Y라는 테넌트에 없습니다. 테넌트의 관리자가 응용 프로그램을 설치하지 않았거나 테넌트의 사용자가 동의하지 않은 경우에 발생할 수 있습니다. 잘못된 테넌트에 인증 요청을 보냈을 수도 있습니다.|
| 80001| 사용할 수 있는 인증 에이전트가 없습니다.|
| 80002| 인증 에이전트의 암호 유효성 검사 요청 시간이 초과되었습니다.|
| 80003| 인증 에이전트에서 받은 응답이 잘못되었습니다.|
| 80004| 로그인 요청에 잘못된 UPN(사용자 계정 이름)이 사용되었습니다.|
| 80005| 인증 에이전트: 오류가 발생했습니다.|
| 80007| 인증 에이전트에서 Active Directory에 연결할 수 없습니다.|
| 80010| 인증 에이전트에서 암호를 해독할 수 없습니다.|
| 81001| 사용자의 Kerberos 티켓이 너무 큽니다.|
| 81002| 사용자의 Kerberos 티켓에 대한 유효성을 검사할 수 없습니다.|
| 81003| 사용자의 Kerberos 티켓에 대한 유효성을 검사할 수 없습니다.|
| 81004| Kerberos 인증 시도가 실패했습니다.|
| 81008| 사용자의 Kerberos 티켓에 대한 유효성을 검사할 수 없습니다.|
| 81009| 사용자의 Kerberos 티켓에 대한 유효성을 검사할 수 없습니다.|
| 81010| 사용자의 Kerberos 티켓이 만료되었거나 잘못되었으므로 Seamless SSO가 실패했습니다.|
| 81011| 사용자의 Kerberos 티켓 정보에 기반하여 사용자 개체를 찾을 수 없습니다.|
| 81012| Azure AD에 로그인하려는 사용자가 장치에 로그인한 사용자와 다릅니다.|
| 81013| 사용자의 Kerberos 티켓 정보에 기반하여 사용자 개체를 찾을 수 없습니다.|
| 90014| 예상된 필드가 자격 증명에 없는 다양한 경우에 사용됩니다.|
| 90093| 요청에 대해 사용할 수 없는 오류 코드와 함께 반환된 그래프입니다.|



## <a name="next-steps"></a>다음 단계

자세한 내용은 [Azure Active Directory 포털의 로그인 활동 보고서](active-directory-reporting-activity-sign-ins.md)를 참조하세요.


