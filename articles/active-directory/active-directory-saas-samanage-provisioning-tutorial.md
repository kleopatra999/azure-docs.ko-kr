---
title: "자습서: Azure Active Directory를 사용한 자동 사용자 프로비전을 위한 Samanage 구성 | Microsoft Docs"
description: "사용자 계정을 Samanage로 자동으로 프로비전 및 프로비전 해제하도록 Azure Active Directory를 구성하는 방법을 알아봅니다."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.translationtype: HT
ms.sourcegitcommit: bde1bc7e140f9eb7bb864c1c0a1387b9da5d4d22
ms.openlocfilehash: 278ebf464fbe815568fbe332f80d5ea6b29e1811
ms.contentlocale: ko-kr
ms.lasthandoff: 07/21/2017

---

# <a name="tutorial-configuring-samanage-for-automatic-user-provisioning"></a>자습서: 자동 사용자 프로비전에 대한 Samanage 구성


이 자습서의 목적은 사용자 계정을 Azure AD에서 Samanage로 자동으로 프로비전 및 프로비전 해제하도록 Samanage 및 Azure AD에서 수행해야 하는 단계를 설명하는 것입니다. 

## <a name="prerequisites"></a>필수 조건

이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.

*   Azure Active Directory 테넌트
*   [Professional 계획](https://www.samanage.com/pricing/) 이상을 사용하도록 설정한 Samanage 테넌트 
*   관리자 권한이 있는 Samanage의 사용자 계정 

> [!NOTE]
> Azure AD 프로비전 통합에서는 [Samanage REST API](https://www.samanage.com/api/)를 사용하며, 이 API는 Samanage 팀이 Professional 계획 이상에서 사용할 수 있습니다.

## <a name="assigning-users-to-samanage"></a>Samanage에 사용자 할당

Azure Active Directory는 "할당"이라는 개념을 사용하여 어떤 사용자가 선택한 앱에 대한 액세스를 받아야 하는지를 판단합니다. 자동 사용자 계정 프로비전의 컨텍스트에서는 Azure AD의 응용 프로그램에 "할당된" 사용자 및 그룹만 동기화됩니다. 

프로비전 서비스를 구성하고 사용하도록 설정하기 전에 Samanage 앱에 액세스해야 하는 사용자를 나타내는 Azure AD의 사용자 및/또는 그룹을 결정해야 합니다. 결정했으면 다음 지침에 따라 이러한 사용자를 Samanage 앱에 할당할 수 있습니다.

[엔터프라이즈 앱에 사용자 또는 그룹 할당](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-samanage"></a>Samanage에 사용자를 할당하기 위한 주요 팁

*   단일 Azure AD 사용자를 Samanage에 할당하여 프로비전 구성을 테스트하는 것이 좋습니다. 추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.

*   Samanage에 사용자를 할당할 때 [할당] 대화 상자에서 **사용자** 역할이나 다른 유효한 응용 프로그램 관련 역할(사용 가능한 경우)을 선택해야 합니다. **기본 액세스** 역할은 프로비전에 적합하지 않으므로 이러한 사용자는 건너뜁니다.

> [!NOTE]
> 추가 기능으로 프로비전 서비스는 Samanage에 정의된 사용자 정의 역할을 읽고 Azure AD로 가져오므로 [역할 선택] 대화 상자에서 이러한 역할을 선택할 수 있습니다. 이러한 역할은 프로비전 서비스를 사용하도록 설정하고 하나의 동기화 주기가 완료된 후 Azure Portal에 표시됩니다.

## <a name="configuring-user-provisioning-to-samanage"></a>Samanage에 사용자 프로비전 구성 

이 섹션에서는 사용자의 Azure AD를 Samanage의 사용자 계정 프로비전 API에 연결하고, Azure AD의 사용자 및 그룹 할당을 기반으로 Samanage에서 할당된 사용자 계정을 만들고 업데이트하고 비활성화하도록 프로비전 서비스를 구성하는 방법을 안내합니다.

> [!TIP]
> [Azure Portal](https://portal.azure.com)에 제공된 지침에 따라 Samanage에 SAML 기반 Single Sign-On을 사용하도록 설정할 수도 있습니다. Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.


### <a name="configure-automatic-user-account-provisioning-to-samanage-in-azure-ad"></a>Azure AD에서 Samanage에 자동 사용자 계정 프로비전 구성:


1. [Azure Portal](https://portal.azure.com)에서 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션으로 이동합니다.

2. 이미 Samanage에 Single Sign-On을 구성한 경우 검색 필드를 사용하여 Samanage의 인스턴스를 검색합니다. 그러지 않은 경우 **추가**를 선택하고 응용 프로그램 갤러리에서 **Samanage**를 검색합니다. 검색 결과에서 Samanage를 선택하고 응용 프로그램 목록에 추가합니다.

3. Samanage의 인스턴스를 선택한 다음 **프로비전** 탭을 선택합니다.

4. **프로비전 모드**를 **자동**으로 설정합니다.

    ![Samanage 프로비전](./media/active-directory-saas-samanage-provisioning-tutorial/Samanage1.png)

5. **관리자 자격 증명** 섹션에 Samanage 계정의 **관리자 사용자 이름 및 관리자 암호**를 입력합니다. 

6. Azure Portal에서 **연결 테스트**를 클릭하여 Azure AD가 Samanage 앱에 연결할 수 있는지 확인합니다. 연결에 실패하면 Samanage 계정에 관리자 권한이 있는지 확인하고 5단계를 다시 시도합니다.

7. 프로비전 오류 알림을 받을 개인 또는 그룹의 메일 주소를 **알림 메일** 필드에 입력하고 “오류가 발생할 경우 메일 알림 보내기” 확인란을 선택합니다.

8. **Save**를 클릭합니다. 

9. [매핑] 섹션에서 **Synchronize Azure Active Directory Users to Samanage**(Azure Active Directory 사용자를 Samanage에 동기화)를 선택합니다.

10. **특성 매핑** 섹션에서 Azure AD에서 Samanage로 동기화되는 사용자 특성을 검토합니다. **일치** 속성으로 선택한 특성은 업데이트 작업 시 Samanage의 사용자 계정을 일치시키는 데 사용됩니다. 저장 단추를 선택하여 변경 내용을 커밋합니다.

11. Samanage에 대한 Azure AD 프로비전 서비스를 사용하도록 설정하려면 **설정** 섹션에서 **프로비전 상태**를 **켜기**로 변경합니다.

12. **Save**를 클릭합니다. 

[사용자 및 그룹] 섹션에서 Samanage에 할당된 모든 사용자 및/또는 그룹의 초기 동기화가 시작됩니다. 초기 동기화는 서비스가 실행되는 동안 약 20분마다 발생하는 차후 동기화보다 더 많은 시간이 걸립니다. **동기화 세부 정보** 섹션을 사용하여 진행 상태를 모니터링하고 링크를 클릭하여 프로비전 서비스에서 수행한 모든 작업을 설명하는 프로비전 작업 보고서를 확인할 수 있습니다.

Azure AD 프로비저닝 로그를 읽는 방법에 대한 자세한 내용은 [자동 사용자 계정 프로비저닝에 대한 보고](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)를 참조하세요.


## <a name="additional-resources"></a>추가 리소스

* [엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리](active-directory-enterprise-apps-manage-provisioning.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>다음 단계

* [프로비전 활동에 대한 로그를 검토하고 보고서를 받아 보는 방법을 살펴봅니다](active-directory-saas-provisioning-reporting.md).

