<properties 
    pageTitle="자습서: Azure Active Directory와 Zoom 통합 | Microsoft Azure" 
    description="Azure Active Directory에서 Zoom을 사용하여 Single Sign-On, 자동화 프로비전 등을 사용하도록 설정하는 방법을 알아봅니다." 
    services="active-directory" 
    authors="jeevansd"  
    documentationCenter="na" 
    manager="femila"/>
<tags 
    ms.service="active-directory" 
    ms.devlang="na" 
    ms.topic="article" 
    ms.tgt_pltfrm="na" 
    ms.workload="identity" 
    ms.date="05/25/2016" 
    ms.author="jeedes" />

#자습서: Azure Active Directory와 Zoom 통합
  
이 자습서에서는 Azure와 Zoom의 통합을 보여줍니다. 이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.

-   유효한 Azure 구독
-   Zoom 테넌트
  
이 자습서를 완료하면, Zoom에 할당한 Azure AD 사용자들은 Zoom 회사 사이트(로그온을 시작한 서비스 공급자)에서 또는, [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 사용하여 응용 프로그램에 Single Sign-On할 수 있습니다.
  
이 자습서에 설명된 시나리오는 다음 구성 요소로 이루어져 있습니다.

1.  Zoom에 응용 프로그램 통합 사용
2.  Single Sign-On 구성
3.  사용자 프로비전 구성
4.  사용자 할당

![시나리오](./media/active-directory-saas-zoom-tutorial/IC784693.png "시나리오")

##Zoom에 응용 프로그램 통합 사용
  
이 섹션에서는 Zoom에 응용 프로그램 통합 사용 방법을 설명합니다.

###Zoom에 응용 프로그램 통합을 사용하려면, 다음 단계를 수행합니다.

1.  Azure 클래식 포털의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.

    ![Active Directory](./media/active-directory-saas-zoom-tutorial/IC700993.png "Active Directory")

2.  **디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.

3.  응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램**을 클릭합니다.

    ![응용 프로그램](./media/active-directory-saas-zoom-tutorial/IC700994.png "응용 프로그램")

4.  페이지 맨 아래에 있는 **추가**를 클릭합니다.

    ![응용 프로그램 추가](./media/active-directory-saas-zoom-tutorial/IC749321.png "응용 프로그램 추가")

5.  **원하는 작업을 선택하세요.** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.

    ![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-zoom-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")

6.  **검색 상자**에서 **Zoom**을 입력합니다.

    ![응용 프로그램 갤러리](./media/active-directory-saas-zoom-tutorial/IC784694.png "응용 프로그램 갤러리")

7.  결과 창에서 **Zoom**을 선택하고**완료**를 눌러 응용 프로그램을 추가합니다.

    ![Zoom](./media/active-directory-saas-zoom-tutorial/IC784695.png "Zoom")

##Single Sign-On 구성
  
이 섹션에서는 SAML 프로토콜 기반 페더레이션을 사용하여 사용자가 Azure AD 계정으로 Zoom에 인증하는 방법을 설명합니다. 이 절차의 일부로 base-64로 인코딩된 인증서 파일을 만들어야 합니다. 이 절차를 잘 모르는 경우 [이진 인증서를 텍스트 파일로 변환하는 방법](http://youtu.be/PlgrzUZ-Y1o)을 참조하십시오.

###Single Sign-On을 구성하려면 다음 단계를 수행합니다.

1.  Azure 클래식 포털의 **Zoom** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성** 대화 상자를 엽니다.

    ![Single Sign-On 구성](./media/active-directory-saas-zoom-tutorial/IC784696.png "Single Sign-On 구성")

2.  **Zoom에 대한 사용자 로그온 방법을 선택하십시오** 페이지에서 **Microsoft Azure AD Single Sign-On**을 선택하고 **다음**을 클릭합니다.

    ![Single Sign-On 구성](./media/active-directory-saas-zoom-tutorial/IC784697.png "Single Sign-On 구성")

3.  **Zoom 로그인 URL** 텍스트 상자의 **앱 URL 구성**에서 "**http://company.zoom.us*" 패턴을 사용하여 URL을 입력한 후, **다음**을 클릭합니다.

    ![앱 URL 구성](./media/active-directory-saas-zoom-tutorial/IC784698.png "앱 URL 구성")

4.  **Zoom에서 Single Sign-On 구성** 페이지에서, **인증서 다운로드**를 클릭하여 컴퓨터에 인증서 파일을 저장합니다.

    ![Single Sign-On 구성](./media/active-directory-saas-zoom-tutorial/IC784699.png "Single Sign-On 구성")

5.  다른 웹 브라우저 창에서 관리자 권한으로 Zoom 회사 사이트에 로그인 합니다.

6.  **Single Sign-On** 탭을 클릭합니다.

    ![SSO(Single sign-on)](./media/active-directory-saas-zoom-tutorial/IC784700.png "SSO(Single sign-on)")

7.  **보안 제어**를 클릭하고, **Single Sign-On**설정으로 이동합니다.

8.  Single Sign-On 섹션에서 다음 단계를 수행 합니다.

    ![SSO(Single sign-on)](./media/active-directory-saas-zoom-tutorial/IC784701.png "SSO(Single sign-on)")

    1.  Azure 클래식 포털의 **Zoom에서 Single Sign-On 설정** 대화 상자 페이지에서 **Single Sign-On 서비스 URL** 값을 복사하여, **로그인 페이지 URL** 텍스트 상자에 붙여넣습니다.
    2.  Azure 클래식 포털의 **Zoom에서 Single Sign-On 설정** 대화 상자 페이지에서**Single Sign-Out 서비스 URL** 값을 복사하여 **로그아웃 페이지 URL** 텍스트 상자에 붙여넣습니다.
    3.  다운로드한 인증서에서 **Base-64로 인코딩된** 파일을 만듭니다.  

        >[AZURE.TIP] 자세한 내용은 [이진 인증서를 텍스트 파일로 변환하는 방법](http://youtu.be/PlgrzUZ-Y1o)을 참조하십시오.

    4.  Base 64로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음 **ID 공급자 인증서** 텍스트 상자에 붙여넣습니다.
    5.  Azure 클래식 포털의 **Zoom에서 Single Sign-On 설정** 대화 상자 페이지에서**발급자 URL** 값을 복사하여 **발급자** 텍스트 상자에 붙여넣습니다.
    6.  **저장**을 클릭합니다.

9.  Azure 클래식 포털에서 Single Sign-On 구성 확인을 선택하고 **완료**를 클릭하여 **Single Sign-On 구성** 대화 상자를 닫습니다.

    ![Single Sign-On 구성](./media/active-directory-saas-zoom-tutorial/IC784702.png "Single Sign-On 구성")

##사용자 프로비전 구성
  
Azure AD 사용자가 Zoom에 로그인할 수 있도록 하려면 사용자 계정이 ZScaler로 프로비전되어야 합니다 Zoom의 경우, 수동으로 프로비전합니다.

###사용자 계정을 프로비전하려면 다음 단계를 수행합니다.

1.  관리자 권한으로 **Zoom** 회사 사이트로 로그인합니다.

2.  **계정 관리** 탭을 클릭 후, **사용자 관리**를 클릭합니다.

3.  사용자 관리 섹션에서 **사용자 추가**를 클릭합니다.

    ![사용자 관리](./media/active-directory-saas-zoom-tutorial/IC784703.png "사용자 관리")

4.  **사용자 추가**페이지에서 다음 단계를 수행합니다.

    ![사용자 추가](./media/active-directory-saas-zoom-tutorial/IC784704.png "사용자 추가")

    1.  **사용자 유형**으로 **기본** 선택
    2.  **이메일** 텍스트 상자에 프로비전 하려는 유효한 AAD 계정의 이메일 주소를 입력합니다.
    3.  **추가**를 클릭합니다.

>[AZURE.NOTE] 다른 Zoom 사용자 계정 생성 도구 또는 Zoom에서 제공하는 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.

##사용자 할당
  
구성을 테스트하려면 응용 프로그램 사용을 허용하려는 Azure AD 사용자를 할당하여 액세스 권한을 부여해야 합니다.

###사용자를 Zoom에 할당하려면 다음 단계를 수행합니다.

1.  Azure 클래식 포털에서 테스트 계정을 만듭니다.

2.  **Zoom **응용 프로그램 통합 페이지에서 **사용자 할당**을 클릭합니다.

    ![사용자 할당](./media/active-directory-saas-zoom-tutorial/IC784705.png "사용자 할당")

3.  테스트 사용자를 선택하고 **할당**을 클릭한 다음 **예**를 클릭하여 할당을 확인합니다.

    ![예](./media/active-directory-saas-zoom-tutorial/IC767830.png "예")
  
Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하십시오.

<!---HONumber=AcomDC_0601_2016-->