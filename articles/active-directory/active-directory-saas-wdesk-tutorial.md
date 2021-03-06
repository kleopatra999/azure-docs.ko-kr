---
title: "자습서: Wdesk와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Wdesk 간에 Single Sign-On을 구성하는 방법을 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.translationtype: Human Translation
ms.sourcegitcommit: a643f139be40b9b11f865d528622bafbe7dec939
ms.openlocfilehash: 37660b80cfb01d6a3105aea5ce248f1e03c46695
ms.contentlocale: ko-kr
ms.lasthandoff: 05/31/2017


---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a>자습서: Wdesk와 Azure Active Directory 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 Wdesk를 통합하는 방법에 대해 알아봅니다.

Wdesk를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.

- Wdesk에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.
- 사용자가 해당 Azure AD 계정으로 Wdesk에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.
- 단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.

Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

Wdesk와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.

- Azure AD 구독
- Wdesk Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.

이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.

1. 갤러리에서 Wdesk 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-wdesk-from-the-gallery"></a>갤러리에서 Wdesk 추가
Wdesk의 Azure AD 통합을 구성하려면 갤러리의 Wdesk를 관리되는 SaaS 앱 목록에 추가해야 합니다.

**갤러리에서 Wdesk를 추가하려면 다음 단계를 수행합니다.**

1. **[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다. 

    ![Active Directory][1]

2. **엔터프라이즈 응용 프로그램**으로 이동합니다. 그런 후 **모든 응용 프로그램**으로 이동합니다.

    ![응용 프로그램][2]
    
3. 새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.

    ![응용 프로그램][3]

4. 검색 상자에 **Wdesk**를 입력합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. 결과 창에서 **Wdesk**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Wdesk에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Wdesk 사용자가 누구인지 알고 있어야 합니다. 즉, Azure AD 사용자와 Wdesk의 관련 사용자 간에 연결이 형성되어야 합니다.

이 연결 관계는 Azure AD의 **사용자 이름** 값을 Wdesk의 **Username** 값으로 할당하여 설정합니다.

Wdesk에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.

1. **[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.
3. **[Wdesk 테스트 사용자 만들기](#creating-a-wdesk-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Wdesk에 만듭니다.
4. **[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.
5. **[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Wdesk 응용 프로그램에서 Single Sign-On을 구성합니다.

**Wdesk에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**

1. Azure Portal의 **Wdesk** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.

    ![Single Sign-on 구성][4]

2. **Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. **Wdesk 도메인 및 URL** 섹션에서 **IDP 시작 모드**로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    a. **식별자** 텍스트 상자에서 `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>` 패턴을 사용하여 URL을 입력합니다.

    b. **회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`

4. **고급 URL 설정 표시**를 선택합니다. **SP** 시작 모드로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    **로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`
     
    > [!NOTE] 
    > 이러한 값은 실제 값이 아닙니다. 이러한 값을 실제 식별자, 회신 URL 및 로그온 URL로 업데이트합니다. SSO를 구성할 때 WDesk 포털에서 이러한 값을 가져옵니다. 
  
5. **SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. 다른 웹 브라우저 창에서 Wdesk에 보안 관리자로 로그인합니다.

8. 왼쪽 아래에서 **관리**를 클릭하고 **계정 관리자**를 선택합니다.
 
     ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. Wdesk 관리에서 **보안**, **SAML** > **SAML 설정**으로 이동합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. **일반 설정**에서 **SAML Single Sign On 사용**을 선택합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. **서비스 공급자 세부 정보**에서 다음 단계를 수행합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      a. **로그인 URL**을 복사한 후 Azure Portal의 **로그온 URL** 텍스트 상자에 붙여 넣습니다.
   
      b. **메타데이터 URL**을 복사한 후 Azure Portal의 **식별자** 텍스트 상자에 붙여 넣습니다.
       
      c. **소비자 URL**을 복사한 후 Azure Portal의 **회신 URL** 텍스트 상자에 붙여 넣습니다.
   
      d. Azure Portal에서 **저장**을 클릭하여 변경 내용을 저장합니다.      

12. **IdP 설정 구성**을 클릭하여 **IdP 설정 편집** 대화 상자를 엽니다. **파일 선택**을 클릭하여 Azure Portal에서 저장한 **Metadata.xml** 파일을 찾습니다.
    
    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. **변경 내용 저장**을 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> 이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.  **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다. 포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.

![Azure AD 사용자 만들기][100]

**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**

1. **Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. 사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. **사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. **사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    a. **이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.

    b. **사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.

    c. **암호 표시**를 선택하고 **암호** 값을 적어둡니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-wdesk-test-user"></a>Wdesk 테스트 사용자 만들기

Azure AD 사용자가 Wdesk에 로그인할 수 있도록 하려면 Wdesk로 프로비전되어야 합니다. Wdesk의 경우, 수동으로 프로비전합니다.

**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**

1. 보안 관리자 권한으로 Wdesk에 로그인합니다.
2. **관리** > **계정 관리자**로 이동합니다.

     ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. **피플** 아래에서 **구성원**을 클릭합니다.

4. 이제 **구성원 추가**를 클릭하여 **구성원 추가** 대화 상자를 엽니다. 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. **사용자** 텍스트 상자에 **brittasimon@contoso.com** 과 같은 사용자의 사용자 이름을 입력하고 **계속** 단추를 클릭합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  아래와 같이 세부 정보를 입력합니다.
  
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    a. **전자 메일** 텍스트 상자에 **brittasimon@contoso.com** 와 같은 사용자의 전자 메일 주소를 입력합니다.

    b. **이름** 텍스트 상자에 사용자의 이름(예: **Britta**)을 입력합니다.

    c. **성** 텍스트 상자에 사용자의 성(예: **Simon**)을 입력합니다.

7. **구성원 저장** 단추를 클릭합니다.  

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-the-azure-ad-test-user"></a>Azure AD 테스트 사용자 할당

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Wdesk에 대한 액세스 권한을 부여합니다.

![사용자 할당][200] 

**Britta Simon을 Wdesk에 할당하려면 다음 단계를 수행합니다.**

1. Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.

    ![사용자 할당][201] 

2. 응용 프로그램 목록에서 **Wdesk**를 선택합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. 왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.

액세스 패널에서 Wdesk 타일을 클릭하면 Wdesk 응용 프로그램에 자동으로 로그온됩니다.
액세스 패널에 대한 자세한 내용은 [Azure 시작](active-directory-saas-access-panel-introduction.md)을 참조하세요.


## <a name="additional-resources"></a>추가 리소스

* [Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png


