<properties
	pageTitle="자습서: Novatus와 Azure Active Directory 통합 | Microsoft Azure"
	description="Azure Active Directory와 Novatus 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
	services="active-directory"
	documentationCenter=""
	authors="jeevansd"
	manager="stevenpo"
	editor=""/>

<tags
	ms.service="active-directory"
	ms.workload="identity"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="04/26/2016"
	ms.author="jeedes"/>


# 자습서: Novatus와 Azure Active Directory 통합

이 자습서에서는 Novatus와 Azure AD(Azure Active Directory)를 통합하는 방법을 보여 줍니다.

Novatus를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.

- Novatus에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.
- 사용자가 해당 Azure AD 계정으로 Novatus에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.
- 단일 중앙 위치인 Azure 클래식 포털에서 계정을 관리할 수 있습니다.

Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.

## 필수 조건

Novatus와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.

- Azure AD 구독
- Novatus Single Sign-on이 설정된 구독


> [AZURE.NOTE] 이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.


이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.


## 시나리오 설명
이 자습서는 테스트 환경에서 Azure AD Single Sign-on을 테스트하는 데 도움을 주기 위해 제공되었습니다.

이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.

1. 갤러리에서 Novatus 추가
2. Azure AD Single Sign-on 구성 및 테스트


## 갤러리에서 Novatus 추가
Novatus의 Azure AD 통합을 구성하려면 갤러리의 Novatus를 관리되는 SaaS 앱 목록에 추가해야 합니다.

**갤러리에서 Novatus를 추가하려면 다음 단계를 수행합니다.**

1. **Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다. 

	![Active Directory][1]

2. **디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.

3. 응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램**을 클릭합니다.

	![응용 프로그램][2]

4. 페이지 맨 아래에 있는 **추가**를 클릭합니다.

	![응용 프로그램][3]

5. **원하는 작업을 선택하세요.** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.

	![응용 프로그램][4]

6. 검색 상자에서 **Novatus**를 입력합니다.
 
	![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_01.png)

7. 결과 창에서 **Novatus**를 선택하고 **완료**를 클릭하여 응용 프로그램을 추가합니다.

	![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_02.png)

##  Azure AD Single Sign-on 구성 및 테스트
이 섹션은 "Britta Simon"이라는 테스트 사용자를 기반으로 Novatus에서 Azure AD Single Sign-On을 구성하고 테스트하는 방법을 보여 주기 위해 작성되었습니다.

Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Novatus 사용자가 누군지 알고 있어야 합니다. 즉, Azure AD 사용자와 Novatus의 관련 사용자 간에 연결이 형성되어야 합니다.

이 연결 관계는 Azure AD의 **사용자 이름** 값을 Novatus의 **Username** 값으로 할당하여 설정합니다.

Novatus에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.
4. **[Novatus 테스트 사용자 만들기](#creating-a-Novatus-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Novatus에 만듭니다.
5. **[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.
5. **[Single Sign-On 테스트](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.

### Azure AD Single Sign-On 구성

이 섹션은 Azure 클래식 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 Novatus 응용 프로그램에서 Single Sign-On을 구성하는 방법을 설명하기 위한 것입니다.



**Novatus에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**

1. Azure 클래식 포털의 **Novatus** 응용 프로그램 통합 페이지에서 **Single Sign-on 구성**을 클릭하여 **Single Sign-on 구성** 대화 상자를 엽니다.

	![Single Sign-On 구성][6]

2. **Novatus에 대한 사용자 로그온 방법 선택** 페이지에서 **Azure AD Single Sign-On**을 선택하고 **다음**을 클릭합니다.

	![Single Sign-On 구성](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_03.png)

3. **앱 설정 구성** 대화 상자 페이지에서 다음 단계를 수행합니다.

	![Single Sign-On 구성](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_04.png)


    a. 로그인 URL 텍스트 상자에 **“https://sso.novatuscontracts.com/companyname”**의 패턴을 사용하여 사용자가 Novatus 응용 프로그램에 로그인하는 데 사용할 URL을 입력합니다. **companyname**을 실제 이름으로 교체해야 하는 일반 이름을 참조하는 경우


4. **Novatus의 Single Sign-On 구성** 페이지에서 다음 단계를 수행합니다.

	![Single Sign-On 구성](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_05.png)

    a. **인증서 다운로드**를 클릭하고 파일을 컴퓨터에 저장합니다.

    b. **다음**을 클릭합니다.


5. 응용 프로그램에 대해 SSO를 구성하려면 jvinci@novatusinc.com를 통해 Novatus 지원 팀에 문의하세요. 다운로드한 인증서 파일을 메일에 첨부하고 해당하는 쪽에 SSO를 설정하기 위해 Novatus 팀과 메타데이터 URL(엔터티 ID, SSO 로그인 URL 및 로그아웃 URL)을 공유합니다.


6. Azure 클래식 포털에서 Single Sign-On 구성 확인을 선택하고 **다음**을 클릭합니다.

	![Azure AD Single Sign-On][10]

7. **Single Sign-On 확인** 페이지에서 **완료**를 클릭합니다.

	![Azure AD Single Sign-On][11]




### Azure AD 테스트 사용자 만들기
이 섹션의 목적은 Azure 클래식 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.



![Azure AD 사용자 만들기][20]

**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**

1. **Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.

	![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-novatus-tutorial/create_aaduser_09.png)

2. **디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.

3. 사용자 목록을 표시하려면 위쪽 메뉴에서 **사용자**를 클릭합니다.

	![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-novatus-tutorial/create_aaduser_03.png)

4. **사용자 추가** 대화 상자를 열려면 아래쪽 도구 모음에서 **사용자 추가**를 클릭합니다.

	![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-novatus-tutorial/create_aaduser_04.png)

5. **이 사용자에 대한 정보 입력** 대화 상자 페이지에서 다음 단계를 수행합니다.

	![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-novatus-tutorial/create_aaduser_05.png)

    a. 사용자 유형에서 조직의 새 사용자를 선택합니다.

    b. 사용자 이름 **텍스트 상자**에 **BrittaSimon**을 입력합니다.

    c. **다음**을 클릭합니다.

6.  **사용자 프로필** 대화 상자 페이지에서 다음 단계를 수행합니다.

	![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-novatus-tutorial/create_aaduser_06.png)

    a. **이름** 텍스트 상자에 **Britta**를 입력합니다.

    b. **성** 텍스트 상자에 **Simon**을 입력합니다.

    c. **표시 이름** 텍스트 상자에 **Britta Simon**을 입력합니다.

    d. **역할** 목록에서 **사용자**를 선택합니다.

    e. **다음**을 클릭합니다.

7. **임시 암호 가져오기** 대화 상자 페이지에서 **만들기**를 클릭합니다.

	![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-novatus-tutorial/create_aaduser_07.png)

8. **임시 암호 가져오기** 대화 상자 페이지에서 다음 단계를 수행합니다.

	![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-novatus-tutorial/create_aaduser_08.png)

    a. **새 암호** 값을 적어둡니다.

    b. **완료**를 클릭합니다.



### Novatus 테스트 사용자 만들기

이 섹션은 Novatus에서 Britta Simon이라는 사용자를 만들기 위한 것입니다. Novatus는 적시에 프로비전을 지원하며 기본적으로 사용하도록 설정합니다.

이 섹션에 작업 항목이 없습니다. 새 사용자가 아직 존재하지 않는 경우 Novatus에 액세스하는 동안 만들어질 수 있습니다. [Azure AD Single Sign-On 구성](#configuring-azure-ad-single-single-sign-on)

> [AZURE.NOTE] 사용자를 수동으로 만들어야 하는 경우 Novatus 지원 팀에 문의해야 합니다.


### Azure AD 테스트 사용자 할당

이 섹션은 Britta Simon에게 Novatus에 대한 액세스 권한을 부여하여 Single Sign-On을 사용할 수 있도록 하기 위한 것입니다.

![사용자 할당][200]

**Britta Simon을 Novatus에 할당하려면 다음 단계를 수행합니다.**

1. Azure 클래식 포털에서 응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램**을 클릭합니다.

	![사용자 할당][201]

2. 응용 프로그램 목록에서 **Novatus**를 선택합니다.

	![Single Sign-On 구성](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_50.png)

1. 위쪽의 메뉴에서 **사용자**를 클릭합니다.

	![사용자 할당][203]

1. 사용자 목록에서 **Britta Simon**을 선택합니다.

2. 아래쪽 도구 모음에서 **할당**을 클릭합니다.

	![사용자 할당][205]



### Single Sign-On 테스트

이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.

액세스 패널에서 Novatus 타일을 클릭하면 Novatus 응용 프로그램에 자동으로 로그온됩니다.


## 추가 리소스

* [Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_205.png

<!---HONumber=AcomDC_0511_2016-->