---
title: "Azure 구독과 Azure Active Directory의 연관 관계 | Microsoft Docs"
description: "Microsoft Azure 로그인 및 Azure 구독과 Azure Active Directory 간의 관계와 같은 관련 문제입니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: bc4773c2-bc4a-4d21-9264-2267065f0aea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
ms.translationtype: HT
ms.sourcegitcommit: 25e4506cc2331ee016b8b365c2e1677424cf4992
ms.openlocfilehash: b2f8cc774b6cc245a4000e5c6924a8bb817707bc
ms.contentlocale: ko-kr
ms.lasthandoff: 08/24/2017

---
# <a name="how-azure-subscriptions-are-associated-with-azure-active-directory"></a>Azure 구독과 Azure Active Directory의 연관 관계
이 문서에서는 Microsoft Azure 로그인 및 Azure 구독과 Azure Active Directory(Azure AD) 간의 관계에 대한 정보를 제공합니다.

## <a name="your-azure-subscriptions-relationship-to-azure-ad"></a>Azure AD에 대한 Azure 구독의 관계
Azure 구독은 Azure AD와 트러스트 관계가 있습니다. 즉, 사용자, 서비스 및 장치를 인증하는 디렉터리를 신뢰합니다. 여러 구독에서 동일한 디렉터리를 신뢰할 수 있지만 각 구독은 하나의 디렉터리만 신뢰합니다. 

구독이 디렉터리와 갖는 트러스트 관계는 구독이 Azure의 다른 리소스(웹 사이트, 데이터베이스 등)와 갖는 관계와 다릅니다. 구독이 만료되면 구독과 연결된 다른 리소스에 대한 액세스도 중지됩니다. 하지만 디렉터리는 Azure에 남아 있으며 해당 디렉터리와 다른 구독을 연결하여 디렉터리 사용자를 계속 관리할 수 있습니다.

![구독과 다이어그램의 연관 관계](./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png)

Azure AD는 Azure 구독에 있는 다른 서비스처럼 작동하지 않습니다. 다른 Azure 서비스는 Azure 구독에 종속됩니다. 하지만 Azure AD에서 표시되는 항목은 구독에 따라 달라지지 않습니다. 로그인한 사용자에 따라 디렉터리에 액세스할 수 있습니다.

모든 사용자는 자신을 인증하는 단일 홈 디렉터리를 가지고 있지만 다른 디렉터리의 게스트가 될 수도 있습니다. Azure AD에서 사용자 계정이 멤버인 디렉터리만 볼 수 있습니다. 디렉터리는 온-프레미스 Active Directory와 동기화될 수도 있습니다.

## <a name="azure-ad-and-cloud-service-subscriptions"></a>Azure AD 및 클라우드 서비스 구독
Azure AD는 다음을 포함하여 대부분의 Microsoft 클라우드 서비스 뒤에 핵심 디렉터리 및 ID 관리 기능을 제공합니다.

* Azure
* Microsoft Office 365
* Microsoft Dynamics CRM Online
* Microsoft Intune

이러한 Microsoft 클라우드 서비스 중 하나에 등록하면 Azure AD 서비스를 체험할 수 있습니다. Azure AD 디렉터리에 Azure 구독을 더 추가하려는 경우 Microsoft 계정으로 로그인한 경우에만 수행할 수 있습니다. 예를 들어, Microsoft 계정을 사용하여 Azure에 등록하고 회사 또는 학교 계정을 사용하여 다른 Microsoft 클라우드 서비스에 등록하는 경우 Azure AD의 두 인스턴스가 있습니다.
1. Azure 구독에 대한 기본 디렉터리입니다. Azure에서 인증될 수 있으므로 Microsoft 계정으로 로그인한 경우 이 디렉터리 또는 만든 다른 디렉터리에 다른 Azure 구독을 추가할 수 있습니다.
2. 회사 또는 학교 계정에 대한 홈 디렉터리입니다. 회사 또는 학교 계정으로 Azure에 로그인한 경우 회사 또는 학교 계정을 Azure에서 직접 인증할 수 없기 때문에 기존 디렉터리에 Azure 구독을 추가할 수 없습니다. 
 
Azure 구독의 관리자를 변경하는 방법을 자세히 알아보려면 [다른 계정에 Azure 구독의 소유권 이전](../billing/billing-subscription-transfer.md)을 참조하세요.

## <a name="suggestions-to-manage-both-a-subscription-and-a-directory"></a>구독 및 디렉터리를 모두 관리하기 위한 제안
Azure 구독의 관리 역할은 Azure 구독에 연결된 리소스를 관리합니다. 이 섹션에서는 Azure 구독 관리자와 Azure AD 디렉터리 관리자 간의 차이점을 설명합니다. 관리자 역할 및 구독을 관리하기 위해 해당 역할을사용하는 다른 제안은 [Azure Active Directory의 관리자 역할 할당](active-directory-assign-admin-roles.md)에서 다룹니다.

등록할 때 기본적으로 서비스 관리자 역할이 할당됩니다. 다른 사용자가 동일한 구독을 사용하여 로그인하고 서비스에 액세스해야 하는 경우 공동 관리자로 추가할 수 있습니다. 

Azure AD는 디렉터리 및 ID 관련 기능을 관리하는 다른 관리 역할 집합을 가지고 있습니다. 예를 들어 디렉터리의 전역 관리자는 디렉터리에 사용자 및 그룹을 추가하거나 사용자에 대해 다단계 인증을 요구할 수 있습니다. 디렉터리를 만든 사용자는 전역 관리자 역할에 할당되어 다른 사용자에게 관리자 역할을 할당할 수 있습니다. 또한 Azure AD 관리 역할은 Office 365 및 Microsoft Intune과 같은 다른 서비스에서도 사용됩니다. 

Azure 구독 관리자와 Azure AD 디렉터리 관리자는 서로 다른 역할입니다. 
* Azure 구독 관리자는 Azure에서 리소스를 관리하고 Azure Portal에서 Azure AD를 사용할 수 있습니다(Azure Portal 자체가 Azure 리소스이기 때문). 
* 디렉터리 관리자는 Azure AD 디렉터리에서만 속성을 관리할 수 있습니다.

역할을 모두 담당할 수 있지만 그럴 필요는 없습니다. 사용자는 디렉터리 전역 관리자 역할에 할당될 수 있지만 Azure 구독의 공동 관리자 또는 서비스 관리자로 할당될 수는 없습니다. 구독 관리자가 아니어도 사용자는 Azure Portal에 로그인할 수 있지만 포털에서 해당 구독의 디렉터리를 관리할 수 없습니다. 이 사용자는 Azure AD PowerShell 또는 Office 365 관리 센터와 같은 다른 도구를 사용하여 디렉터리를 관리할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* Azure 구독의 관리자를 변경하는 방법을 자세히 알아보려면 [다른 계정에 Azure 구독의 소유권 이전](../billing/billing-subscription-transfer.md)을 참조하세요.
* Microsoft Azure에서 리소스 액세스를 제어하는 방법에 대해 자세히 알아보려면 [Azure의 리소스 액세스 이해](active-directory-understanding-resource-access.md)
* Azure AD에서 역할을 할당하는 방법에 대한 자세한 내용은 [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles-azure-portal.md)

<!--Image references-->
[1]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_PassThruAuth.png
[2]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png
[3]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_SignInDisambiguation.PNG

