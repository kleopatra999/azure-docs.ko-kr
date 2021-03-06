---
title: "Azure Active Directory B2B 공동 작업 초대 전자 메일의 요소 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업 초대 전자 메일 템플릿"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.translationtype: Human Translation
ms.sourcegitcommit: a30a90682948b657fb31dd14101172282988cbf0
ms.openlocfilehash: 458a2cab13b7e83f120e0926a95d454070181dfb
ms.contentlocale: ko-kr
ms.lasthandoff: 05/25/2017


---


# <a name="the-elements-of-the-b2b-collaboration-invitation-email"></a>B2B 공동 작업 초대 전자 메일의 요소

초대 전자 메일은 온보드의 파트너를 Azure AD에서 B2B 공동 작업 사용자로 불러오기 위한 중요한 구성 요소입니다. 받는 사람의 신뢰를 높이는 데 사용할 수 있습니다. 전자 메일에 적법성과 사회적 증거를 전자 메일에 추가하여 받는 사람이 안심하고 **시작** 단추를 선택하여 초대를 수락할 수 있습니다. 이 신뢰는 공유 마찰을 줄이는 데 핵심적입니다. 또한 이 템플릿을 통해 전자 메일도 보기 좋게 구성할 수 있습니다.

![Azure AD B2b 초대 전자 메일](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-the-email"></a>전자 메일 설명
전자 메일의 몇 가지 요소를 확인하여 이러한 기능을 최대한 활용하는 방법에 대해 살펴보겠습니다.

### <a name="subject"></a>제목
전자 메일의 제목은 다음 패턴을 따릅니다. &lt;tenantname&gt; 조직에 초대되었습니다.

### <a name="from-address"></a>보낸 사람 주소
보낸 사람 주소에 대해서는 LinkedIn 유사 패턴을 사용합니다.  초대자가 누구인지와 어떤 회사에 소속되어 있는지를 명확히 하고 전자 메일이 Microsoft 전자 메일 주소에서 전송된 것인지를 명확히 해야 합니다. 형식: &lt;tenantname&gt;(Microsoft를 통해) <invites@microsoft.com&gt;의 &lt;초대자 표시 이름&gt;

### <a name="reply-to"></a>회신
회신 전자 메일은 사용 가능할 때 초대자의 전자 메일로 설정되므로 전자 메일에 회신하면 초대자에게 전자 메일이 다시 전송됩니다.

### <a name="branding"></a>브랜딩
테넌트에서 보낸 초대 전자 메일은 테넌트에 대해 설정했을 수 있는 회사 브랜딩을 사용합니다. 이 기능을 활용하려는 경우 자세한 구성 방법은 [다음](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal)과 같습니다. 전자 메일에 배너 로고가 나타납니다. 최상의 결과를 얻으려면 [여기](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal)에 제공되는 이미지 크기 및 품질 지침을 따르세요. 또한 회사 이름이 활용 방안에도 표시됩니다.

### <a name="call-to-action"></a>활용 방안
활용 방안은 받는 사람이 메일을 받은 이유에 대한 설명과 받는 사람이 요청 받은 작업의 두 부분으로 구성됩니다.
- "이유" 섹션은 다음 패턴을 사용하여 처리될 수 있습니다. &lt;tenantname&gt; 조직에서 응용 프로그램에 액세스하도록 초대되었습니다.

- 또한 "요청되는 작업" 섹션은 **시작** 단추의 존재 여부에 따라 결정됩니다. 초대 받을 필요가 없는 받는 사람이 추가되면 이 단추가 표시되지 않습니다.

### <a name="inviters-information"></a>초대자에 대한 정보
초대자의 표시 이름이 전자 메일에 포함됩니다. 또한 Azure AD 계정에 대해 프로필 사진을 설정한 경우 초대 전자 메일에 해당 사진도 포함됩니다. 두 가지 항목 모두 전자 메일에 대한 받는 사람의 신뢰도를 높이기 위한 것입니다.

자신의 프로필 사진을 아직 설정하지 않은 경우 다음과 같이 사진 대신 초대자의 이니셜이 있는 아이콘이 표시됩니다.

  ![초대자의 이니셜 표시](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a>body
본문에는 초대자가 작성했거나 초대 API를 통해 전달된 메시지가 포함됩니다. 이것은 텍스트 영역에 불과하며, 보안상의 이유로 HTML 태그를 처리하지 않습니다.

### <a name="footer-section"></a>바닥글 섹션
바닥글에는 Microsoft 회사 브랜드가 포함되며, 받는 사람은 이를 통해 전자 메일이 모니터링되지 않은 별칭에서 전송되었는지 여부를 알 수 있습니다. 특수 사례:

- 초대자에게 초대 테넌시의 전자 메일 주소가 없습니다.

  ![초대자 사진에 초대 테넌시의 전자 메일 주소가 없습니다.](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- 받는 사람이 초대를 충전할 필요가 없습니다.

  ![받는 사람이 초대를 충전할 필요가 없는 경우](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a>다음 단계

Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:

* [Azure AD B2B 공동 작업이란?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법은 무엇입니까?](active-directory-b2b-admin-add-users.md)
* [정보 작업자가 B2B 공동 작업 사용자를 추가하는 방법은 무엇입니까?](active-directory-b2b-iw-add-users.md)
* [B2B 공동 작업 초대 상환](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B 공동 작업 라이선스](active-directory-b2b-licensing.md)
* [Azure Active Directory B2B 공동 작업 문제 해결](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B 공동 작업 자주 묻는 질문(FAQ)](active-directory-b2b-faq.md)
* [Azure Active Directory B2B 공동 작업 API 및 사용자 지정](active-directory-b2b-api.md)
* [B2B 공동 작업 사용자에 대한 다단계 인증](active-directory-b2b-mfa-instructions.md)
* [초대 없이 B2B 공동 작업 사용자 추가](active-directory-b2b-add-user-without-invite.md)
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)

