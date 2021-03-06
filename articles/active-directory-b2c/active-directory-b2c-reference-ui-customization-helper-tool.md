<properties
	pageTitle="Azure Active Directory B2C 미리 보기: 페이지 UI 사용자 지정 도우미 도구 | Microsoft Azure"
	description="Azure Active Directory B2C에서 페이지 UI 사용자 지정 기능을 설명하기 위해 사용된 도우미 도구"
	services="active-directory-b2c"
	documentationCenter=""
	authors="swkrish"
	manager="msmbaldwin"
	editor="bryanla"/>

<tags
	ms.service="active-directory-b2c"
	ms.workload="identity"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="06/06/2016"
	ms.author="swkrish"/>

# Azure Active Directory B2C 미리 보기: 페이지 UI(사용자 인터페이스) 사용자 지정 기능을 설명하기 위해 사용된 도우미 도구

이 문서는 Azure AD(Azure Active Directory) B2C의 [주요 UI 사용자 지정 문서](active-directory-b2c-reference-ui-customization.md)에 동반됩니다. 다음 단계는 제공되는 샘플 HTML 및 CSS 콘텐츠를 사용하여 페이지 UI 사용자 지정 기능을 연습하는 방법을 설명합니다.

[AZURE.INCLUDE [active-directory-b2c-preview-note](../../includes/active-directory-b2c-preview-note.md)]

## Azure AD B2C 테넌트 가져오기

사용자 지정을 수행하기 전에 Azure AD B2C 테넌트가 없다면 [Azure AD B2C 테넌트를 가져와](active-directory-b2c-get-started.md)야 합니다.

## 등록 정책 만들기

제공된 샘플 콘텐츠는 [등록 정책](active-directory-b2c-reference-policies.md#how-to-create-a-sign-up-policy)의 두 페이지, 즉 [ID 공급자 선택 페이지](active-directory-b2c-reference-ui-customization.md#identity-provider-selection-page) 및 [로컬 계정 등록 페이지](active-directory-b2c-reference-ui-customization.md#local-account-sign-up-page)를 사용자 지정합니다. [등록 정책을 만드는](active-directory-b2c-reference-policies.md#how-to-create-a-sign-up-policy) 경우 로컬 계정(메일 주소), Facebook, 및 Google+를 **ID 공급자**로 추가합니다. 샘플 HTML 콘텐츠에서는 이 항목만을 IDP로 수용합니다.

## 응용 프로그램 등록

정책을 실행하는 데 사용할 수 있는 B2C 테넌트에 [응용 프로그램을 등록](active-directory-b2c-app-registration.md)해야 합니다. 응용 프로그램을 등록한 후 등록 정책을 실제로 실행하는데 사용할 수 있는 옵션이 몇 가지 있습니다.

- [응용 프로그램의 등록 및 로그인 사용자](active-directory-b2c-overview.md#getting-started)의 “시작” 섹션에 나열된 Azure AD B2C 빠른 시작 응용 프로그램 중 하나를 빌드합니다.
- 미리 빌드해 놓은 [Azure AD B2C 실습](https://aadb2cplayground.azurewebsites.net) 응용 프로그램을 사용합니다. 실습을 사용하기로 선택하는 경우 **리디렉션 URI** `https://aadb2cplayground.azurewebsites.net/`을 사용하여 B2C 테넌트에 응용 프로그램을 등록해야 합니다.
- [Azure 포털](https://portal.azure.com/)에서 정책의 **지금 실행** 단추를 사용합니다.

## 정책 사용자 지정

정책의 모양과 느낌을 사용자 지정하려면 우선 Azure AD B2C의 특정 규칙을 사용하여 HTML 및 CSS 파일을 만들어야 합니다. 그 후 정적 콘텐츠를 Azure AD B2C에서 액세스할 수 있도록 공개적으로 사용 가능한 위치로 업로드할 수 있습니다. 사용자 전용 웹 서버, Azure Blob 저장소, Azure 콘텐츠 배달 네트워크 또는 그 밖의 고정 리소스 호스팅 공급자일 수 있습니다. HTTPS를 통해 콘텐츠를 사용할 수 있고 CORS를 사용하여 액세스할 수 있어야 한다는 것이 유일한 요구 사항입니다. 정적 콘텐츠를 웹에 노출한 후에는 이 위치를 가리키도록 정책을 편집하여 고객에게 해당 콘텐츠를 제공할 수 있습니다. [주요 UI 사용자 지정 문서](active-directory-b2c-reference-ui-customization.md)는 Azure AD B2C 사용자 지정 기능이 작동하는 방식에 대해 자세히 설명합니다.

이 자습서에 대한 일부 샘플 콘텐츠를 이미 만들어서 Azure Blob 저장소에 호스팅해 두었습니다. 샘플 콘텐츠는 "Contoso B2C"라는 가상의 회사를 테마로 하는 매우 기본적인 사용자 지정입니다. 사용자의 정책으로 시도해 보려면 다음 단계를 따릅니다.

1. [Azure 포털](https://portal.azure.com/)의 테넌트에 로그인하고 B2C 기능 블레이드로 이동합니다.
2. **등록 정책**을 클릭한 다음 사용자의 등록 정책(예: "b2c\_1\_sign\_up")을 클릭합니다.
3. **페이지 UI 사용자 지정** 및 **ID 공급자 선택 페이지**를 차례로 클릭합니다.
4. **사용자 지정 템플릿 사용** 스위치를 **예**로 설정/해제합니다. **사용자 지정 페이지 URI** 필드에서 `https://contosob2c.blob.core.windows.net/static/Index.html`을 입력합니다. **확인**을 클릭합니다.
5. **로컬 계정 등록 페이지**를 클릭합니다. **사용자 지정 템플릿 사용** 스위치를 **예**로 설정/해제합니다. **사용자 지정 페이지 URI** 필드에서 `https://contosob2c.blob.core.windows.net/static/EmailVerification.html`을 입력합니다. **확인**을 두 번 클릭하여 UI 사용자 지정 블레이드를 닫습니다.
6. **Save**를 클릭합니다.

이제 사용자가 지정한 정책을 사용해 볼 수 있습니다. 사용자의 응용 프로그램이나 원한다면 Azure AD B2C 실습을 사용할 수 있을 뿐만 아니라 정책 블레이드에서 **지금 실행** 명령을 클릭만 할 수도 있습니다. 드롭다운 상자에서 응용 프로그램을 선택하고 적절한 리디렉션 URI를 선택합니다. **지금 실행** 단추를 클릭합니다. 새 브라우저 탭이 열리고 준비된 새 컨텐츠로 응용 프로그램에 등록한 사용자 환경을 실행할 수 있습니다.

## 샘플 콘텐츠를 Azure Blob 저장소에 업로드합니다.

Azure Blob 저장소를 사용하여 페이지 콘텐츠를 호스팅하려는 경우, 저장소 계정을 만들고 B2C 도우미 도구를 사용하여 파일을 업로드할 수 있습니다.

### 저장소 계정 만들기

1. [Azure 포털](https://portal.azure.com/)에 로그인합니다.
2. **+새로 만들기** > **데이터 + 저장소** > **저장소 계정**을 클릭합니다. Azure Blob 저장소 계정을 만들려면 Azure 구독이 필요합니다. [Azure 웹 사이트](https://azure.microsoft.com/pricing/free-trial/)에서 무료 평가판에 등록할 수 있습니다.
3. 저장소 계정에 **이름**(예: "contoso")을 제공하고 **가격 책정 계층**, **리소스 그룹** 및 **구독**에 적절한 항목을 선택합니다. **시작 보드에 고정** 옵션이 선택되었는지 확인합니다. **만들기**를 클릭합니다.
4. 시작 보드에 돌아가서 방금 만든 저장소 계정을 클릭합니다.
5. **요약** 섹션에서 **컨테이너** 및 **+추가**를 차례로 클릭합니다.
6. 컨테이너에 **이름**을 제공하고(예: "b2c") **Blob**를 **액세스 형식**으로 선택합니다. **확인**을 클릭합니다.
7. 만든 컨테이너는 **Blob** 블레이드에서 목록에 표시됩니다. 컨테이너의 URL을 적어둡니다. 예를 들어 `https://contoso.blob.core.windows.net/b2c`와 유사한 모양이어야 합니다. **Blob** 블레이드를 닫습니다.
8. 저장소 계정 블레이드에서 **키**를 클릭하고 **저장소 계정 이름** 및 **기본 선택키** 필드의 값을 적어둡니다.

> [AZURE.NOTE]
	**기본 선택키**는 중요한 보안 자격 증명입니다.

### 도우미 도구 및 샘플 파일을 다운로드합니다.

[Azure Blob 저장소 도우미 도구 및 샘플 파일(.zip 파일)](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip)을 다운로드하거나 GitHub에서 복제할 수 있습니다.

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

이 리포지토리는 예제 HTML, CSS 및 이미지를 포함하는 `sample_templates\contoso` 디렉터리를 포함합니다. 이러한 템플릿에서 Azure Blob 저장소 계정을 참조하도록 하려면 HTML 파일을 편집해야 합니다. `Index.htnml` 및 `EmailValidation.html`을 열어서 `https://localhost` 인스턴스를 위 단계에서 적어둔 컨테이너의 URL로 교체합니다. 이런 경우 `https://login.microsoftonline.com` 도메인의 Azure AD에서 HTML이 제공되기 때문에 HTML 파일의 절대 경로를 사용해야 합니다.

### 샘플 파일 업로드

동일한 리포지토리에서 `B2CAzureStorageClient.zip`의 압축을 풀고 그 안에 포함된 `B2CAzureStorageClient.exe` 파일을 실행합니다. 이 프로그램은 저장소 계정에 사용자가 지정한 디렉터리의 모든 파일을 업로드하고 해당 파일에 대한 CORS 액세스가 가능하도록 합니다. 위 단계를 따랐다면 HTML 및 CSS 파일은 이제 사용자의 저장소 계정을 가리킵니다. 저장소 계정 이름은 `blob.core.windows.net` 앞에 오는 부분(예: `contoso`)입니다. 브라우저에서 `https://{storage-account-name}.blob.core.windows.net/{container-name}/Index.html`에 액세스를 시도하여 콘텐츠를 제대로 업로드했는지 확인할 수 있습니다. 또한 [http://test-cors.org/](http://test-cors.org/)를 사용하여 콘텐츠가 사용하도록 설정된 CORS인지 확인합니다. (결과에서 "XHR 상태: 200"을 찾습니다.)

### 정책 사용자 지정 다시 하기

사용자의 저장소 계정에 샘플 콘텐츠를 업로드한 후에는 이를 참조하도록 등록 정책을 편집해야 합니다. 이번에는 사용자 저장소 계정의 URL을 사용하여 위 ["정책 사용자 지정"](#customize-your-policy) 섹션의 단계를 반복합니다. 예를 들어 `Index.html` 파일의 위치는 `<url-of-your-container>/Index.html`이 되어야 합니다.

이제 **지금 실행** 단추 또는 자체 응용 프로그램을 사용하여 정책을 다시 실행할 수 있습니다. 두 경우 모두 동일한 샘플 HTML 및 CSS를 사용했으므로 결과는 거의 동일한 모양이어야 합니다. 하지만 사용자의 정책은 자신의 Azure Blob 저장소 인스턴스를 참조하며 원하는 대로 파일을 편집하고 다시 업로드할 수 있습니다. HTML 및 CSS 사용자 지정에 대한 자세한 내용은 [주요 UI 사용자 지정 문서](active-directory-b2c-reference-ui-customization.md)를 참조하세요.

<!---HONumber=AcomDC_0608_2016-->