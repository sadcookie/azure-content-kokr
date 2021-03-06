<properties
	pageTitle="IoT Hub를 사용하여 클라우드-장치 메시지 보내기 | Microsoft Azure"
	description="이 자습서에 따라 Java에서 Azure IoT Hub를 사용하여 클라우드-장치 메시지를 보내는 방법을 알아봅니다."
	services="iot-hub"
	documentationCenter="java"
	authors="dominicbetts"
	manager="timlt"
	editor=""/>

<tags
     ms.service="iot-hub"
     ms.devlang="java"
     ms.topic="article"
     ms.tgt_pltfrm="na"
     ms.workload="na"
     ms.date="06/23/2016"
     ms.author="dobett"/>

# 자습서: IoT Hub 및 Java를 사용하여 클라우드-장치 메시지를 보내는 방법

[AZURE.INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## 소개

Azure IoT Hub는 수백만의 IoT 장치와 응용 프로그램 백 엔드 간에 안정적이고 안전한 양방향 통신이 가능하도록 지원하는 완전히 관리되는 서비스입니다. [IoT Hub 시작] 자습서에서 IoT Hub를 만들어 그 안에 장치 ID를 프로비전하고 장치-클라우드 메시지를 보내는 시뮬레이트된 장치를 코딩하는 방법을 볼 수 있습니다.

이 자습서는 [IoT Hub 시작하기]를 토대로 작성되었습니다. 단일 장치에 클라우드-장치 메시지를 보내는 방법 및 IoT Hub에서 배달 승인(*피드백*)을 요청하고 응용 프로그램 클라우드 백 엔드에서 이를 수신하는 방법을 보여 줍니다.

클라우드-장치 메시지에 자세한 정보는 [IoT Hub 개발자 가이드][IoT Hub Developer Guide - C2D]에서 찾아볼 수 있습니다.

이 자습서의 끝 부분에서는 다음 두 개의 Java 콘솔 응용 프로그램을 실행합니다.

* **simulated-device**는 [IoT Hub 시작]에서 만든 앱의 수정된 버전으로서 IoT Hub에 연결하고 클라우드-장치 메시지를 수신합니다.
* **send-c2d-messages**는 IoT Hub를 통해 시뮬레이트된 장치에 클라우드-장치 메시지를 보낸 다음 배달 승인을 받습니다.

> [AZURE.NOTE] IoT Hub는 많은 장치 플랫폼 및 언어(C, Java 및 Javascript 포함)를 위해 비록 Azure IoT 장치 SDK이지만 SDK를 지원합니다. 이 자습서의 코드 및 일반적으로 Azure IoT Hub에 장치를 연결하는 방법에 대한 단계별 지침은 [Azure IoT 개발자 센터]를 참조하세요.

이 자습서를 완료하려면 다음이 필요합니다.

+ Java SE 8. <br/> [개발 환경 준비][lnk-dev-setup]는 Windows 또는 Linux에서 이 자습서에 대한 Java를 설치하는 방법을 설명합니다.

+ Maven 3. <br/> [개발 환경 준비][lnk-dev-setup]는 Windows 또는 Linux에서 이 자습서에 대한 Maven을 설치하는 방법을 설명합니다.

+ 활성 Azure 계정. 계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 평가판][lnk-free-trial]을 참조하세요.

## 시뮬레이션된 장치에서 메시지 받기

이 섹션에서는 [IoT Hub 시작]에서 만든 시뮬레이트된 장치 응용 프로그램을 수정하여 IoT Hub로부터 클라우드-장치 메시지를 수신합니다.

1. 텍스트 편집기를 사용하여 simulated-device\\src\\main\\java\\com\\mycompany\\app\\App.java 파일을 엽니다.

2. **App** 클래스 안에 중첩 클래스로 다음과 같은 **MessageCallback** 클래스를 추가합니다. 장치가 IoT Hub에서 메시지를 받을 때 **실행** 메서드가 호출됩니다. 이 예제에서 장치는 항상 허브에 메시지를 완료했음을 알립니다.

    ```
    private static class MessageCallback implements
    com.microsoft.azure.iothub.MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));

        return IotHubMessageResult.COMPLETE;
      }
    }
    ```

3. 다음과 같이 클라이언트를 열기 전에 **main** 메서드를 수정하여 **MessageCallback** 인스턴스를 만들고 **setMessageCallback** 메서드를 호출합니다.

    ```
    client = new DeviceClient(connString, protocol);

    MessageCallback callback = new MessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [AZURE.NOTE] 전송으로 AMQP 대신 HTTP/1을 사용하는 경우 **DeviceClient** 인스턴스는 IoT Hub의 메시지를 자주(25분 미만 마다) 확인합니다. AMQP와 HTTP/1 지원 간의 차이점 및 IoT Hub 제한에 대한 자세한 내용은 [IoT Hub 개발자 가이드][IoT Hub Developer Guide - C2D]를 참조하세요.

## 앱 백 엔드에서 클라우드-장치 메시지 보내기

이 섹션에서는 클라우드-장치 메시지를 시뮬레이트된 장치 앱으로 보내는 Java 콘솔 응용 프로그램을 만듭니다. [IoT Hub 시작] 자습서에서 추가된 장치의 장치 ID 및 에서 찾을 수 있는 IoT Hub에 대한 연결 문자열이 필요합니다.

1. 명령 프롬프트에서 다음 명령을 사용하여 **send-c2d-messages**라는 새 Maven 프로젝트를 만듭니다. 이것은 하나의 긴 명령입니다.

    ```
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. 명령 프롬프트에서 새 send-c2d-messages 폴더로 이동합니다.

3. 텍스트 편집기를 사용하여 send-c2d-messages 폴더에서 pom.xml 파일을 열고 **종속성** 노드에 다음 종속성을 추가합니다. 이 옵션을 사용하면 IoT Hub 서비스와 통신하기 위해 응용 프로그램에서 **iothub-java-service-client** 패키지를 사용할 수 있습니다.

    ```
    <dependency>
      <groupId>com.microsoft.azure.iothub-java-client</groupId>
      <artifactId>iothub-java-service-client</artifactId>
      <version>1.0.7</version>
    </dependency>
    ```

4. pom.xml 파일을 저장하고 닫습니다.

5. 텍스트 편집기를 사용하여 send-c2d-messages\\src\\main\\java\\com\\mycompany\\app\\App.java 파일을 엽니다.

6. 파일에 다음 **import** 문을 추가합니다.

    ```
    import com.microsoft.azure.iot.service.sdk.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. **App** 클래스에 다음 클래스 수준 변수를 추가하고 **{yourhubconnectionstring}** 및 **{yourdeviceid}**를 앞에서 기록해둔 값으로 바꿉니다.

    ```
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```
    
8. **main** 메서드를 IoT hub에 연결한 다음 코드로 바꾸고 장치에 메시지를 보낸 다음 장치가 메시지를 수신하고 처리했다는 승인을 기다립니다.

    ```
    public static void main(String[] args) throws IOException,
        URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(
        connectionString, protocol);
      
      if (serviceClient != null) {
        serviceClient.open();
        FeedbackReceiver feedbackReceiver = serviceClient
          .getFeedbackReceiver(deviceId);
        if (feedbackReceiver != null) feedbackReceiver.open();

        Message messageToSend = new Message("Cloud to device message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);

        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent to device");

        FeedbackBatch feedbackBatch = feedbackReceiver.receive(10000);
        if (feedbackBatch != null) {
          System.out.println("Message feedback received, feedback time: "
            + feedbackBatch.getEnqueuedTimeUtc().toString());
        }

        if (feedbackReceiver != null) feedbackReceiver.close();
        serviceClient.close();
      }
    }
    ```

    > [AZURE.NOTE] 간단히 하기 위해 이 자습서에서는 다시 시도 정책을 구현하지 않습니다. 프로덕션 코드에서는 MSDN 문서 [일시적인 오류 처리]에서 제시한 대로 다시 시도 정책(예: 지수 백오프)을 구현해야 합니다.

## 다음 단계

이 자습서에서 클라우드-장치 메시지를 보내고 받는 방법을 알아보았습니다. IoT Hub 기능 및 시나리오는 다음의 자습서와 함께 계속해서 탐색할 수 있습니다.

- [장치-클라우드 메시지 처리]는 장치에서 들어오는 대화형 메시지 및 원격 분석을 안정적으로 처리하는 방법을 보여 줍니다.
- [장치에서 파일 업로드]는 장치에서 파일을 쉽게 업로드하기 위해 클라우드-장치 메시지를 사용하는 패턴을 설명합니다.

IoT Hub에 대한 추가 정보:

* [IoT Hub 개요]
* [IoT Hub 개발자 가이드]
* [IoT Hub 지침]
* [지원하는 장치 플랫폼 및 언어]
* [Azure IoT 개발자 센터]

<!-- Links -->

[IoT Hub 시작]: iot-hub-java-java-getstarted.md
[IoT Hub 시작하기]: iot-hub-java-java-getstarted.md
[IoT Hub Developer Guide - C2D]: iot-hub-devguide.md#c2d
[장치-클라우드 메시지 처리]: iot-hub-csharp-csharp-process-d2c.md
[장치에서 파일 업로드]: iot-hub-csharp-csharp-file-upload.md
[IoT Hub 개요]: iot-hub-what-is-iot-hub.md
[IoT Hub 지침]: iot-hub-guidance.md
[IoT Hub 개발자 가이드]: iot-hub-devguide.md
[지원하는 장치 플랫폼 및 언어]: iot-hub-supported-devices.md
[Azure IoT 개발자 센터]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/get_started/java-devbox-setup.md
[일시적인 오류 처리]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

<!---HONumber=AcomDC_0629_2016-->