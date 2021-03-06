<properties
    pageTitle="Eclipse에서 Java용 Azure 라이브러리 패키지의 Javadoc 콘텐츠 표시"
    description="Eclipse에서 Azure 라이브러리의 Javadoc 콘텐츠를 표시하는 방법입니다."
    services=""
    documentationCenter="java"
    authors="rmcmurray"
    manager="wpickett"
    editor=""/>

<tags
    ms.service="multiple"
    ms.workload="na"
    ms.tgt_pltfrm="multiple"
    ms.devlang="Java"
    ms.topic="article"
    ms.date="06/24/2016" 
    ms.author="robmcm"/>

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->

# Eclipse에서 Java용 Azure 라이브러리 패키지의 Javadoc 콘텐츠 표시 #

Javadoc 콘텐츠를 Java용 Azure 라이브러리 패키지에 연결하면 Java용 Azure 라이브러리 패키지의 Javadoc 콘텐츠를 Eclipse 환경 내에서 볼 수 있습니다. 다음 단계는 Eclipse 내에서 이 기능을 사용하는 방법을 보여 줍니다.

이 절차는 빌드 경로에 Java용 Azure 라이브러리를 이미 추가했다고 가정합니다.

## Eclipse에서 Java용 Azure 라이브러리의 Javadoc 콘텐츠를 표시하려면 ##

* Eclipse의 프로젝트 탐색기에 있는 프로젝트 **참조 라이브러리** 섹션에서 Java JAR용 Azure 라이브러리의 상황에 맞는 메뉴를 엽니다. 예를 들어 **microsoft windowsazure-api 0.1.0.jar**(버전 번호는 설치한 버전에 따라 다를 수 있음)입니다.
* **속성**을 클릭합니다.
* **속성** 대화 상자의 왼쪽 창에서 **Javadoc Location**(Javadoc 위치)을 클릭합니다. **Javadoc Location**(Javadoc 위치) 대화 상자가 표시됩니다.
* **Javadoc URL** 또는 **Javadoc in archive**(보관 중인 Javadoc)를 지정할 수 있습니다.
    * **Javadoc URL** 지정을 선택하는 경우 **http://dl.windowsazure.com/javadoc** 또는 **http://dl.windowsazure.com/storage/javadoc**과 같은 URL을 사용합니다.
    * **Javadoc in archive**(보관 중인 Javadoc)를 사용하도록 선택하는 경우 외부 파일 또는 작업 영역 파일을 지정할 수 있습니다. 필요에 따라 선택하여 찾거나 유효성을 검사합니다. 다음 예제에서는 Java용 Azure 라이브러리를 **c:\\MyAzureJARs**라는 폴더에 로컬로 다운로드된 해당 Javadoc JAR와 연결합니다. ![][ic553487]
* *옵션*: **유효성 검사**를 클릭합니다. Javadoc JAR의 잠재적 문제가 여기에 표시될 수 있습니다.
* **확인**을 클릭합니다.

라이브러리에 연결되면 Javadoc 콘텐츠가 Eclipse IDE 내에 표시됩니다. 예를 들어 `blob`이 코드에서 `CloudBlockBlob` 형식으로 정의되는 경우 다음은 코드에서 `blob.acquireLease`를 입력했을 때 표시되는 Javadoc 콘텐츠의 예입니다.

![][ic553488]

## 참고 항목 ##

[Eclipse용 Azure 도구 키트][]

[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기][]

[Eclipse용 Azure 도구 키트 설치][]

Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터][]를 참조하세요.

<!-- URL List -->

[Azure Java 개발자 센터]: http://go.microsoft.com/fwlink/?LinkID=699547
[Eclipse용 Azure 도구 키트]: http://go.microsoft.com/fwlink/?LinkID=699529
[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기]: http://go.microsoft.com/fwlink/?LinkID=699533
[Eclipse용 Azure 도구 키트 설치]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!---HONumber=AcomDC_0629_2016-->