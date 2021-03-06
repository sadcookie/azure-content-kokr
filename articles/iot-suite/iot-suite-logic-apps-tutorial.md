<properties
  pageTitle="Azure IoT Suite 및 논리 앱 | Microsoft Azure"
  description="논리 앱을 비즈니스 프로세스에 대한 Azure IoT Suite에 연결하는 방법에 대한 자습서입니다."
  services=""
  suite="iot-suite"
  documentationCenter=""
  authors="aguilaaj"
  manager="timlt"
  editor=""/>

<tags
  ms.service="iot-suite"
  ms.devlang="na"
  ms.topic="article"
  ms.tgt_pltfrm="na"
  ms.workload="na"
  ms.date="05/20/2016"
  ms.author="araguila"/>
  
# 자습서: 미리 구성된 Azure IoT Suite 원격 모니터링 솔루션에 논리 앱 연결

미리 구성된 [Microsoft Azure IoT Suite][lnk-internetofthings] 원격 모니터링 솔루션은 IoT 솔루션의 예를 보여 주는 종단 간 기능 집합으로 신속하게 시작할 수 있는 훌륭한 방법입니다. 이 자습서에서는 미리 구성된 Microsoft Azure IoT Suite 원격 모니터링 솔루션에 논리 앱을 추가하는 방법을 안내합니다. IoT 솔루션을 비즈니스 프로세스에 연결하여 어떻게 잘 활용할 수 있는지도 설명합니다.

_미리 구성된 원격 모니터링 솔루션을 프로비전하는 방법을 찾고 있는 경우 [자습서: 미리 구성된 IoT 솔루션 시작][lnk-getstarted]을 참조하세요._

이 자습서를 시작하기 전에 Azure 구독에서 미리 구성된 원격 모니터링 솔루션을 프로비전하는 것 외에도 비즈니스 프로세스를 트리거하는 전자 메일을 보낼 수 있도록 SendGrid 계정을 만들어야 합니다. [SendGrid](https://sendgrid.com/)에서 **무료 평가판**을 클릭하여 무료 평가판 계정을 등록할 수 있습니다. 무료 평가판 계정을 등록한 후에는 SendGrid에서 메일 전송 권한을 부여하는 [API 키](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html)를 만들어야 합니다. 이 API 키는 자습서의 뒷부분에서 필요합니다.

미리 구성된 원격 모니터링 솔루션을 이미 프로비전했다고 가정하고 [Azure 포털][lnk-azureportal]에서 해당 솔루션에 대한 리소스 그룹으로 이동합니다. 리소스 그룹 이름이 원격 모니터링 솔루션을 프로비전할 때 선택한 솔루션 이름과 같습니다. 리소스 그룹에서 솔루션에 대해 미리 프로비전된 모든 Azure 리소스를 볼 수 있습니다(단, Azure 클래식 포털에서 찾을 수 있는 Azure Active Directory 응용 프로그램은 예외). 다음 스크린샷은 미리 구성된 원격 모니터링 솔루션에 대한 예제 **리소스 그룹** 블레이드를 보여 줍니다.

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

시작하려면 미리 구성된 솔루션과 함께 사용할 논리 앱을 설정합니다.

## 논리 앱 설정

1. Azure 포털에서 리소스 그룹 블레이드 맨 위에서 __추가__를 클릭합니다.

2. __논리 앱__을 검색하여 선택한 후 **만들기**를 클릭합니다.

3. __이름__을 입력하고 원격 모니터링 솔루션을 프로비전할 때 사용한 것과 동일한 **구독**, **리소스 그룹**, **앱 서비스 계획**을 사용합니다. __만들기__를 클릭합니다.

    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)

4. 배포가 완료되면 논리 앱이 리소스 그룹에 리소스로 나열됩니다.

5. 논리 앱을 클릭하여 논리 앱 블레이드로 이동하면 **논리 앱 디자이너**가 즉시 열립니다.

    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)

6. __수동 – HTTP 요청을 받은 경우__를 선택합니다. 특정 JSON 형식 페이로드와 함께 들어오는 HTTP 요청이 트리거로 작동함을 지정합니다.

7. 다음을 요청 본문 JSON 스키마에 붙여 넣습니다.

    ```
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
    
    참고: 논리 앱을 저장한 후 HTTP POST에 대한 URL을 복사할 수 있지만 먼저 작업을 추가해야 합니다.

8. 수동 트리거 아래에서 __(+)__를 클릭합니다. 그런 다음 **작업 추가**를 클릭합니다.

    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)

9. **SendGrid - 메일 보내기**를 검색하여 클릭합니다.

    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)

10. 연결 이름(예: **SendGridConnection**)을 입력하고 SendGrid 계정을 설정할 때 만든 **SendGrid Api 키**를 입력하고 **연결 만들기**를 클릭합니다.

    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)

11. 소유한 전자 메일 주소를 **보낸 사람** 및 **받는 사람** 필드에 추가합니다. **원격 모니터링 경고 [DeviceId]**를 **제목** 필드에 추가합니다. **전자 메일 본문** 필드에 **장치 [DeviceId]이(가) 값 [measuredValue]와(과) 함께 [measurementName]을(를) 보고했습니다.**를 추가합니다. **이전 단계에서 데이터를 삽입할 수 있습니다** 섹션을 클릭하여 **[DeviceId]**, **[measurementName]** 및 **[measuredValue]**을(를) 추가할 수 있습니다.

    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)

12. 최상위 메뉴에서 __저장__을 클릭합니다.

13. **HTTP 요청을 받은 경우** 트리거를 클릭하고 __이 URL에 대한 Http Post__ 값을 복사합니다. 이 URL은 자습서의 뒷부분에서 필요합니다.

> [AZURE.NOTE] 논리 앱을 사용하면 Office 365의 작업을 비롯하여 [다양한 유형의 작업][lnk-logic-apps-actions]을 실행할 수 있습니다.

## EventProcessor 웹 작업 설정

이 섹션에서는 미리 구성된 솔루션을, 논리 앱을 트리거하는 URL을 장치 센서 값이 임계값을 초과할 때 실행되는 작업에 추가하여 만든 논리 앱에 연결합니다.

1. git 클라이언트를 사용하여 최신 버전의 [azure-iot-remote-monitoring github 리포지토리][lnk-rmgithub]를 복제합니다. 예:

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. Visual Studio에서 리포지토리의 로컬 복사본에서 __RemoteMonitoring.sln__을 엽니다.

3. **Infrastructure\\Repository** 폴더에서 __ActionRepository.cs__ 파일을 엽니다.

4. 아래와 같이 **actionIds** 사전을 논리 앱에서 기록한 __이 URL에 대한 Http Post__로 업데이트합니다.

    ```
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post to this UR>" },
        { "Raise Alarm", "<Http Post to this UR> }
    };
    ```

5. 변경 내용을 솔루션에 저장하고 Visual Studio를 종료합니다.

## 명령줄에서 배포

이 섹션에서는 Azure에서 현재 실행 중인 버전을 대체하도록 원격 모니터링 솔루션의 업데이트된 버전을 배포합니다.

1. [개발 설정][lnk-devsetup] 지침에 따라 배포 환경을 설정합니다.

2.  로컬로 배포하려면 [로컬 배포][lnk-localdeploy] 지침을 따릅니다.

3.  클라우드로 배포하고 기존 클라우드 배포를 업데이트하려면 [클라우드 배포][lnk-clouddeploy] 지침을 따릅니다. 원래 배포의 이름을 배포 이름으로 사용합니다. 예를 들어 원래 배포가 **demologicapp**였다면 다음 명령을 사용합니다.

    ``
    build.cmd cloud release demologicapp
    ``
    
    빌드 스크립트를 실행하는 경우 처음으로 솔루션을 프로비전했을 때 사용한 것과 동일한 Azure 계정, 구독, 지역 및 Active Directory 인스턴스를 사용해야 합니다.

## 작업에서 논리 앱 참조

솔루션을 처음으로 프로비전할 때 미리 구성된 원격 모니터링 솔루션에는 기본적으로 두 개의 규칙이 설정되어 있습니다. 두 규칙 모두 **SampleDevice001** 장치에 있습니다.

* 온도 > 38.00
* 습도 > 48.00

온도 규칙은 **경보 발생** 작업을 트리거하고 습도 규칙은 **SendMessage** 작업을 트리거합니다. **ActionRepository** 클래스의 작업 모두에 동일한 URL을 사용했다고 가정할 경우 논리 앱은 두 규칙 중 하나를 트리거하고 SendGrid를 사용하여 경고 정보가 포함된 전자 메일을 **받는 사람** 주소로 보냅니다.

> [AZURE.NOTE] 임계값에 도달할 때마다 논리 앱이 계속 트리거되므로 불필요한 전자 메일을 피하려면 솔루션 포털에서 규칙을 사용하지 않도록 설정하거나 [Azure 포털][lnk-azureportal]에서 논리 앱을 사용하지 않도록 설정할 수 있습니다.

전자 메일을 받는 것 외에도 논리 앱이 포털에서 실행될 때 다음을 확인할 수 있습니다.

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## 다음 단계

이제 논리 앱을 사용하여 미리 구성된 솔루션을 비즈니스 프로세스에 연결했으며 [미리 구성된 솔루션 사용자 지정][lnk-customize] 또는 [물리적 장치를 솔루션에 추가하는 방법][lnk-connect]에 대해 자세히 알아볼 수 있습니다.

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-connect]: iot-suite-connecting-devices.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md

<!---HONumber=AcomDC_0525_2016-->