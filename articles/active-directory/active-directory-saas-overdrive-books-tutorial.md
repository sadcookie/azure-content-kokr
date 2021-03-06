<properties 
    pageTitle="자습서: Overdrive Books와 Azure Active Directory 통합 | Microsoft Azure" 
    description="Azure Active Directory에서 Overdrive Books를 사용하여 Single Sign-On, 자동화된 프로비전 등을 사용하도록 설정하는 방법을 알아봅니다." 
    services="active-directory" 
    authors="jeevansd"  
    documentationCenter="na" 
    manager="stevenpo"/>
<tags 
    ms.service="active-directory" 
    ms.devlang="na" 
    ms.topic="article" 
    ms.tgt_pltfrm="na" 
    ms.workload="identity" 
    ms.date="01/14/2016" 
    ms.author="jeedes" />

#자습서: Overdrive Books와 Azure Active Directory 통합
  
이 자습서는 Azure 및 OverDrive의 통합을 보여주기 위한 것입니다. 이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.

-   유효한 Azure 구독
-   OverDrive Single Sign-On이 설정된 구독
  
이 자습서를 완료한 후 OverDrive에 할당한 Azure AD 사용자가 OverDrive 회사 사이트(서비스 공급자가 시작한 로그온)에서 또는 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 사용하여 응용 프로그램에 Single Sign-On할 수 있습니다.
  
이 자습서에 설명된 시나리오는 다음 구성 요소로 이루어져 있습니다.

1.  OverDrive에 응용 프로그램 통합 사용
2.  Single Sign-On 구성
3.  사용자 프로비전 구성
4.  사용자 할당

![시나리오](./media/active-directory-saas-overdrive-books-tutorial/IC784462.png "시나리오")
##OverDrive에 응용 프로그램 통합 사용
  
이 섹션은 OverDrive에 응용 프로그램 통합을 사용하도록 설정하는 방법을 간략하게 설명하기 위한 것입니다.

###OverDrive에 응용 프로그램 통합을 사용하도록 설정하려면

1.  Azure 관리 포털의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.

    ![Active Directory](./media/active-directory-saas-overdrive-books-tutorial/IC700993.png "Active Directory")

2.  **디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.

3.  응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램**을 클릭합니다.

    ![응용 프로그램](./media/active-directory-saas-overdrive-books-tutorial/IC700994.png "응용 프로그램")

4.  페이지 맨 아래에 있는 **추가**를 클릭합니다.

    ![응용 프로그램 추가](./media/active-directory-saas-overdrive-books-tutorial/IC749321.png "응용 프로그램 추가")

5.  **원하는 작업을 선택하세요.** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.

    ![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-overdrive-books-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")

6.  **검색 상자**에 **OverDrive**를 입력합니다.

    ![응용 프로그램 갤러리](./media/active-directory-saas-overdrive-books-tutorial/IC784463.png "응용 프로그램 갤러리")

7.  결과 창에서 **OverDrive**를 선택하고 **완료**를 클릭하여 응용 프로그램을 추가합니다.

    ![OverDrive](./media/active-directory-saas-overdrive-books-tutorial/IC799950.png "OverDrive")
##Single Sign-On 구성
  
이 섹션은 사용자가 SAML 프로토콜 기반 페더레이션을 사용하여 Azure AD의 계정으로 OverDrive에 인증할 수 있게 하는 방법을 간략하게 설명하기 위한 것입니다.

###Single Sign-On을 구성하려면 다음 단계를 수행합니다.

1.  Azure AD 포털의 **OverDrive** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성** 대화 상자를 엽니다.

    ![Single Sign-On 사용](./media/active-directory-saas-overdrive-books-tutorial/IC784465.png "Single Sign-On 사용")

2.  **OverDrive에 대한 사용자 로그온 방법을 선택하십시오.** 페이지에서 **Microsoft Azure AD Single Sign-On**을 선택하고 **다음**을 클릭합니다.

    ![Single Sign-On 구성](./media/active-directory-saas-overdrive-books-tutorial/IC784466.png "Single Sign-On 구성")

3.  **앱 URL 구성** 페이지의 **OverDrive 로그인 URL** 텍스트 상자에 다음 패턴 "**http://mslibrarytest.libraryreserve.com*"을 사용하여 URL을 입력한 후 **다음**을 클릭합니다.

    ![앱 URL 구성](./media/active-directory-saas-overdrive-books-tutorial/IC784467.png "앱 URL 구성")

4.  **OverDrive에서 Single Sign-On 구성** 페이지에서 메타데이터 파일을 다운로드한 다음 OverDrive 지원팀에 보냅니다.

    ![Single Sign-On 구성](./media/active-directory-saas-overdrive-books-tutorial/IC784468.png "Single Sign-On 구성")

    >[AZURE.NOTE]OverDrive 지원팀은 Single Sign-On을 구성하고 구성이 완료되면 알림을 보냅니다.

5.  Azure AD 포털에서 Single Sign-On 구성 확인을 선택하고 **완료**를 클릭하여 **Single Sign-On 구성** 대화 상자를 닫습니다.

    ![Single Sign-On 구성](./media/active-directory-saas-overdrive-books-tutorial/IC784469.png "Single Sign-On 구성")
##사용자 프로비전 구성
  
OverDrive를 프로비전하는 사용자를 구성할 작업 항목이 없습니다. 할당된 사용자가 OverDrive에 로그인하려고 하면 필요한 경우 OverDrive 계정이 자동으로 생성됩니다.

>[AZURE.NOTE]다른 OverDrive 사용자 계정 생성 도구 또는 OverDrive가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.

##사용자 할당
  
구성을 테스트하려면 응용 프로그램 사용을 허용하려는 Azure AD 사용자를 할당하여 액세스 권한을 부여해야 합니다.

###OverDrive에 사용자를 할당하려면 다음 단계를 수행합니다.

1.  Azure AD 포털에서 테스트 계정을 만듭니다.

2.  **OverDrive ** 응용 프로그램 통합 페이지에서 **사용자 할당**을 클릭합니다.

    ![사용자 할당](./media/active-directory-saas-overdrive-books-tutorial/IC784470.png "사용자 할당")

3.  테스트 사용자를 선택하고 **할당**을 클릭한 다음 **예**를 클릭하여 할당을 확인합니다.

    ![예](./media/active-directory-saas-overdrive-books-tutorial/IC767830.png "예")
  
Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하십시오.

<!---HONumber=AcomDC_0121_2016-->