<properties 
	pageTitle="Azure 클래식 포털을 사용하여 Azure 미디어 서비스 미디어 콘텐츠를 관리하는 방법" 
	description="Azure 미디어 서비스에서 미디어 콘텐츠를 관리하는 방법에 대해 알아봅니다. 여기에는 업로드, 인덱싱, 인코딩, 암호화 및 게시가 포함됩니다." 
	services="media-services" 
	documentationCenter="" 
	authors="Juliako" 
	manager="erikre" 
	editor=""/>

<tags 
	ms.service="media-services" 
	ms.workload="media" 
	ms.tgt_pltfrm="na" 
	ms.devlang="na" 
	ms.topic="article" 
	ms.date="06/22/2016"  
	ms.author="juliako"/>


# Azure 클래식 포털을 사용하여 Azure 미디어 서비스 콘텐츠 관리


이 항목에서는 Azure 클래식 포털을 사용하여 미디어 서비스 계정의 미디어 콘텐츠를 관리하는 방법을 보여 줍니다.

다음과 같은 콘텐츠 작업을 포털에서 직접 수행하는 방법을 보여 줍니다.

- 게시 상태, 게시된 URL, 크기, 외신 업데이트 날짜/시간, 자산이 암호화되었는지 여부 등과 같은 콘텐츠 정보를 봅니다.
- 새 콘텐츠 업로드
- 콘텐츠 인덱싱
- 콘텐츠 인코딩
- 암호화
- 콘텐츠 게시/게시 취소
- 콘텐츠 재생


##<a id="upload"></a>방법: 콘텐츠 업로드


[AZURE.INCLUDE [media-services-selector-upload-files](../../includes/media-services-selector-upload-files.md)]


1. [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=256666&clcid=0x409)에서 **미디어 서비스**를 클릭한 후 미디어 서비스 계정 이름을 클릭합니다.
2. 콘텐츠 페이지를 선택합니다.
3. 페이지나 포털 맨 아래에 있는 **업로드** 단추를 클릭합니다.
4. **콘텐츠 업로드** 대화 상자에서 원하는 자산 파일로 이동합니다. 파일을 클릭한 후 **열기**를 클릭하거나 **Enter** 키를 누릅니다.

	![UploadContentDialog][uploadcontent]

5. 콘텐츠 업로드 대화 상자에서 확인 단추를 클릭하여 파일 및 콘텐츠 이름을 적용합니다.
6. 업로드가 시작되며, 포털 맨 아래에서 진행 상태를 추적할 수 있습니다.

	![JobStatus][status]

업로드가 완료되면 콘텐츠 목록에 새 자산이 나열됩니다. 편의상 이름의 끝에 "**-Source**"가 추가되어 새 콘텐츠를 인코딩 작업의 원본 콘텐츠로 추적할 수 있게 합니다.

![ContentPage][contentpage]

업로드 프로세스가 중지된 후 파일 크기 값이 업데이트되지 않는 경우 **메타데이터 동기화** 단추를 누릅니다. 그러면 자산 파일 크기가 저장소의 실제 파일 크기와 동기화되고 콘텐츠 페이지의 값이 새로 고쳐집니다.

##<a id="index"></a>방법: 콘텐츠 인덱싱

> [AZURE.SELECTOR]
- [.NET](media-services-index-content.md)
- [포털](media-services-manage-content.md#index)

Azure 미디어 인덱서를 사용하면 미디어 파일 콘텐츠를 검색 가능하게 만들고 선택 자막 및 키워드용 전체 텍스트 기록을 생성할 수 있습니다. 아래에서 설명하는 단계에 따라 Azure 클래식 포털을 사용하여 콘텐츠를 인덱싱할 수 있습니다. 그러나 파일 및 인덱싱 작업 수행 방법을 보다 세부적으로 제어하려는 경우에는 Media Services SDK for .NET이나 REST API를 사용할 수 있습니다. 자세한 내용은 [Azure 미디어 인덱서를 사용하여 미디어 파일 인덱싱](media-services-index-content.md)을 참조하세요.

다음 단계는 Azure 클래식 포털을 사용하여 콘텐츠를 인덱싱하는 방법을 보여 줍니다.

1. 인덱싱하려는 파일을 선택합니다. 파일 형식에 대해 인덱싱이 지원되는 경우에는 콘텐츠 페이지 아래쪽에서 프로세스 단추를 사용할 수 있습니다.
1. 프로세스 단추를 누릅니다.
2. **프로세스** 대화 상자에서 **Azure 미디어 인덱서** 프로세서를 선택합니다.
3. 그런 다음 프로세스 대화 상자에서 입력 미디어 파일의 자세한 **제목** 및 **설명** 정보를 채웁니다.

![Process][process]

##<a id="encode"></a>방법: 콘텐츠 인코딩

> [AZURE.SELECTOR]
- [.NET](media-services-dotnet-encode-asset.md)
- [REST (영문)](media-services-rest-encode-asset.md)
- [포털](media-services-manage-content.md#encode)

인터넷을 통해 디지털 비디오를 배달하려면 미디어를 압축해야 합니다. 미디어 서비스는 콘텐츠를 인코딩할 방법(예: 사용할 코덱, 파일 형식, 해상도, 비트 전송률)을 지정할 수 있는 미디어 인코더를 제공합니다.

Azure 미디어 서비스 작업 시 가장 일반적인 시나리오 중 하나는 클라이언트에 적응 비트 전송률 스트리밍을 제공하는 것입니다. 적응 비트 전송률 스트리밍을 사용하면 현재 네트워크 대역폭, CPU 사용률 및 기타 요인에 따라 비디오가 표시되므로 클라이언트는 더 높거나 낮은 비트 전송률 스트림으로 전환할 수 있습니다. 미디어 서비스에서 지원하는 적응 비트 전송률 스트리밍 기술은 HLS(HTTP 라이브 스트리밍), 부드러운 스트리밍, MPEG DASH 및 HDS(Adobe PrimeTime/Access 정식 사용자만 해당)입니다.

미디어 서비스는 적응 비트 전송률 MP4 또는 부드러운 스트리밍 인코딩 콘텐츠를 미디어 서비스에서 지원되는 스트리밍 형식(MPEG DASH, HLS, 부드러운 스트리밍, HDS)으로 다시 패키지하지 않고도 이런 스트리밍 형식으로 배달할 수 있게 하는 동적 패키징을 제공합니다.

동적 패키징을 이용하려면 다음을 수행해야 합니다.

- mezzanine(원본) 파일을 적응 비트 전송률 MP4 파일 또는 적응 비트 전송률 부드러운 스트리밍 파일 집합으로 인코딩합니다(인코딩 단계는 이 자습서의 뒷부분에서 설명).
- 콘텐츠를 배달하는 출발점이 될 스트리밍 끝점에 하나 이상의 주문형 스트리밍 단위를 구성합니다. 자세한 내용은 [주문형 스트리밍 예약 단위를 확장하는 방법](media-services-manage-origins.md#scale_streaming_endpoints/)을 참조하세요

동적 패키징에서는 단일 저장소 형식으로 파일을 저장하고 비용을 지불하기만 하면 됩니다. 그러면 미디어 서비스가 클라이언트의 요청에 따라 적절한 응답을 빌드 및 제공합니다.

동적 패키징 기능을 사용할 수 있을 뿐만 아니라, 주문형 스트리밍 예약 단위는 200Mbps 단위로 구입할 수 있는 전용 송신 용량을 제공합니다. 기본적으로 주문형 스트리밍은 다른 모든 사용자와 서버 리소스(예: 계산, 송신 기능 등)가 공유되는 공유 인스턴스 모델로 구성되어 있습니다. 주문형 스트리밍 처리량을 개선하려면 주문형 스트리밍 예약 단위를 구입하는 것이 좋습니다.

이 섹션에서는 Azure 클래식 포털을 사용하여 미디어 인코더 표준으로 콘텐츠를 인코드할 수 있는 단계를 설명합니다.

1.  인코딩하려는 파일을 선택합니다.

  이 파일 형식에 대해 이 지원되는 경우에는 콘텐츠 페이지 아래쪽에서 프로세스 단추를 사용할 수 있습니다.
4. **프로세스** 대화 상자에서 **미디어 인코더 표준** 프로세서를 선택합니다.
5. **인코딩 구성** 중에서 하나를 선택합니다.

![Process2][process2]


[미디어 인코더 표준용 태스크 기본 설정 문자열](https://msdn.microsoft.com/library/mt269960) 항목에 각 기본 설정의 의미가 설명되어 있습니다.

5. 그런 다음, 원하는 출력 콘텐츠 이름을 입력하거나 기본값을 적용합니다. 확인 단추를 클릭하여 인코딩 작업을 시작하고 포털 맨 아래에서 진행 상태를 추적할 수 있습니다.
6. 확인을 누릅니다.

인코딩이 완료되고 나면 콘텐츠 페이지에 인코딩된 파일이 포함됩니다.

인코딩 작업의 진행률을 보려면 **작업** 페이지로 전환합니다.

인코딩이 완료된 후 파일 크기 값이 업데이트되지 않는 경우 **메타데이터 동기화** 단추를 누릅니다. 그러면 출력 자산 파일 크기가 저장소의 실제 파일 크기와 동기화되고 콘텐츠 페이지의 값이 새로 고쳐집니다.

##<a id="encrypt"></a>방법: 콘텐츠 암호화


미디어 서비스의 경우 AES 키 또는 PlayReady DRM을 통해 자산을 동적으로 암호화하려는 경우, 다음을 참조하세요.

- mezzanine(원본) 파일을 적응 비트 전송률 MP4 파일 또는 적응 비트 전송률 부드러운 스트리밍 파일 집합으로 인코딩합니다(인코딩 단계는 [인코드](#encode) 섹션에서 설명).
- 콘텐츠를 배달하는 출발점이 될 스트리밍 끝점에 하나 이상의 주문형 스트리밍 단위를 구성합니다. 자세한 내용은 [주문형 스트리밍 예약 단위를 확장하는 방법](media-services-manage-origins.md#scale_streaming_endpoints/)을 참조하세요
- "기본 aes 일반 키 서비스 정책" 또는 "기본 playready 라이선스 서비스 정책"을 구성합니다. 자세한 내용은 [콘텐츠 키 권한 부여 정책 구성](media-services-portal-configure-content-key-auth-policy.md)을 참조하세요.


	암호화를 사용할 준비가 되면 **콘텐츠** 페이지 하단에 있는 **암호화** 단추를 누릅니다.

	![암호화][encrypt]

	암호화를 사용하면 플레이어가 스트림을 요청할 때마다 미디어 서비스에서 AES 또는 PlayReady 암호화를 사용하여 콘텐츠를 동적으로 암호화하는 데 지정된 키를 사용합니다. 스트림을 해독하기 위해 플레이어는 키 배달 서비스에서 키를 요청합니다. 사용자에게 키를 얻을 수 있는 권한이 있는지 여부를 결정하기 위해 서비스는 키에 지정된 권한 부여 정책을 평가합니다.

참고 항목:

- [PlayReady DRM으로 보호](media-services-rest-deliver-streaming-content.md)
- [AES-128 키로 보호](media-services-protect-with-aes128.md)

##<a id="publish"></a>방법: 콘텐츠 게시

> [AZURE.SELECTOR]
- [.NET](media-services-deliver-streaming-content.md)
- [REST (영문)](media-services-rest-deliver-streaming-content.md)
- [포털](media-services-manage-content.md#publish)

###개요

콘텐츠 스트림 또는 다운로드에 사용할 수 있는 URL을 사용자에게 제공하려면 먼저 로케이터를 만들어 자산을 "게시"해야 합니다. 로케이터는 자산에 포함된 파일에 대한 액세스를 제공합니다. 미디어 서비스는 두 가지 유형의 로케이터를 지원합니다.하나는 OnDemandOrigin 로케이터로서 미디어를 스트리밍하는 데 사용되고(예: MPEG DASH, HLS 또는 부드러운 스트리밍) 다른 하나는 SAS(공유 액세스 서명) 로케이터로서 미디어 파일을 다운로드하는 데 사용됩니다.

Azure 클래식 포털을 사용하여 자산을 게시할 때 해당 로케이터가 만들어지며 URL(자산에 .ism 파일이 포함된 경우) 또는 SAS URL을 기반으로 하는 OnDemantOrigin이 제공됩니다.

SAS URL의 형식은 다음과 같습니다.

	{blob container name}/{asset name}/{file name}/{SAS signature}

스트리밍 URL에는 다음 형식이 있으며 부드러운 스트리밍 자산을 재생하는 데 사용할 수 있습니다.

	{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

HLS 스트리밍 URL을 작성하려면 URL에 (format=m3u8-aapl)을 추가합니다.

	{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

MPEG DASH 스트리밍 URL을 작성하려면 URL에 (format=mpd-time-csf)를 추가합니다.

	{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


로케이터에는 만료 날짜가 있습니다. 자산을 게시하기 위해 포털을 사용할 때 만료 날짜가 100년인 로케이터가 만들어집니다.

>[AZURE.NOTE] 2015년 3월 이전에 로케이터를 만드는 데 포털을 사용한 경우에는 만료 날짜가 2년인 로케이터가 생성되었습니다.

로케이터의 만료 날짜를 업데이트하려면 [REST](http://msdn.microsoft.com/library/azure/hh974308.aspx#update_a_locator) 또는 [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API를 사용합니다. SAS 로케이터의 만료 날짜를 업데이트할 때 해당 URL도 변경됩니다.

###게시

자산을 게시하기 위해 포털을 사용하려면 다음을 수행합니다.

1. 자산을 선택합니다.
2. 다음 게시 단추를 클릭합니다.
	
 ![PublishedContent][publishedcontent]


## 방법: 포털에서 콘텐츠 재생

**Azure 클래식 포털**에서는 비디오를 테스트하는 데 사용할 수 있는 콘텐츠 플레이어를 제공합니다.

원하는 비디오를 클릭하고 포털 맨 아래에 있는 **재생** 단추를 클릭합니다.
 
다음과 같은 몇 가지 고려 사항이 적용됩니다.

- 비디오가 게시된 것을 확인합니다.
- **MEDIA SERVICES CONTENT PLAYER**가 기본 스트리밍 끝점에서 재생됩니다. 기본이 아닌 스트리밍 끝점에서 재생하려면 다른 플레이어를 사용합니다. 예를 들어 [Azure 미디어 서비스 플레이어](http://amsplayer.azurewebsites.net/azuremediaplayer.html)를 사용합니다.

![AMSPlayer][AMSPlayer]

##미디어 서비스 학습 경로

[AZURE.INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

##피드백 제공

[AZURE.INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]




<!-- Images -->
[portaloverview]: ./media/media-services-manage-content/media-services-content-page.png
[publishedcontent]: ./media/media-services-manage-content/media-services-upload-content-published.png
[uploadcontent]: ./media/media-services-manage-content/UploadContent.png
[status]: ./media/media-services-manage-content/Status.png
[encoder]: ./media/media-services-manage-content/EncoderDialog2.png
[branding]: ./media/branding-reporting.png
[contentpage]: ./media/media-services-manage-content/media-services-content-page.png
[process]: ./media/media-services-manage-content/media-services-process-video.png
[process2]: ./media/media-services-manage-content/media-services-process-video2.png
[encrypt]: ./media/media-services-manage-content/media-services-encrypt-content.png
[AMSPlayer]: ./media/media-services-manage-content/media-services-portal-player.png

<!---HONumber=AcomDC_0629_2016-->