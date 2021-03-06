<properties 
    pageTitle=".NET 및 AMQP 1.0을 사용한 서비스 버스 | Microsoft Azure"
    description="AMQP를 사용하여 .NET에서 서비스 버스 사용"
    services="service-bus"
    documentationCenter="na"
    authors="sethmanheim"
    manager="timlt"
    editor="" /> 
<tags 
    ms.service="service-bus"
    ms.devlang="na"
    ms.topic="article"
    ms.tgt_pltfrm="na"
    ms.workload="na"
    ms.date="05/06/2016"
    ms.author="sethm" />

# AMQP 1.0을 사용하여 .NET에서 서비스 버스 사용

[AZURE.INCLUDE [service-bus-selector-amqp](../../includes/service-bus-selector-amqp.md)]

## 서비스 버스 SDK 다운로드

AMQP 1.0 지원은 서비스 버스 SDK 버전 2.1 이상에서 이용할 수 있습니다. [NuGet][]에서 최신 서비스 버스 비트를 다운로드할 수 있습니다.

## AMQP 1.0을 사용하여 .NET 응용 프로그램 구성

기본적으로 서비스 버스 .NET 클라이언트 라이브러리는 전용 SOAP 기반 프로토콜을 사용하여 서비스 버스 서비스와 통신합니다. 기본 프로토콜 대신 AMQP 1.0을 사용하려면 다음 섹션에서 설명한 대로 서비스 버스 연결 문자열에서 이를 명시적으로 구성해야 합니다. AMQP 1.0을 사용하는 경우 이러한 변경 사항 외에는 응용 프로그램 코드가 기본적으로 변경되지 않습니다.

현재 릴리스에는 AMQP 사용 시 지원되지 않는 몇 가지 API 기능이 있습니다. 지원되지 않는 이러한 기능은 뒤에 나오는 [지원되지 않는 기능, 제한 및 동작 차이](#unsupported-features-restrictions-and-behavioral-differences) 섹션에 나열되어 있습니다. AMQP를 사용하는 경우 몇 가지 고급 구성 설정도 다른 의미를 가집니다.

### App.config를 사용한 구성

응용 프로그램에서는 App.config 구성 파일을 사용하여 설정을 저장하는 것이 바람직합니다. 서비스 버스 응용 프로그램의 경우 App.config를 사용하여 서비스 버스 **ConnectionString** 값에 대한 설정을 저장할 수 있습니다. 샘플 App.config 파일은 다음과 같습니다.

	<?xml version="1.0" encoding="utf-8" ?>
	<configuration>
	    <appSettings>
	        <add key="Microsoft.ServiceBus.ConnectionString"
	             value="Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp" />
	    </appSettings>
	</configuration>

`Microsoft.ServiceBus.ConnectionString` 설정의 값은 서비스 버스에 대한 연결을 구성하는 데 사용되는 서비스 버스 연결 문자열입니다. 형식은 다음과 같습니다.

	Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp

여기서 `[namespace]` 및 `SharedAccessKey`은(는) [Azure 클래식 포털][]에서 가져옵니다. 자세한 내용은 [서비스 버스 큐를 사용하는 방법][]을 참조하십시오.

AMQP를 사용하는 경우 `;TransportType=Amqp`을(를) 사용하여 연결 문자열을 추가합니다. 이 표기는 AMQP 1.0을 사용하여 서비스 버스에 연결하도록 클라이언트 라이브러리를 알립니다.

## 메시지 직렬화

기본 프로토콜을 사용하는 경우 .NET 클라이언트 라이브러리의 기본 직렬화 동작은 [DataContractSerializer][] 형식을 사용하여 클라이언트 라이브러리와 서비스 버스 서비스 간의 전송에 대한 [BrokeredMessage][] 인스턴스를 직렬화하는 것입니다. AMQP 전송 모드를 사용하는 경우 클라이언트 라이브러리는 [broker 저장 메시지][BrokeredMessage]를 AMQP 메시지로 직렬화에 대해 AMQP 형식 시스템을 사용합니다. 이 직렬화를 통해 서비스 버스에 액세스하기 위해 JMS API를 사용하는 Java 응용 프로그램과 같은 다른 플랫폼에서 잠재적으로 실행하는 응용 프로그램 수신을 통해 메시지를 수신하고 해석합니다.

[BrokeredMessage][] 인스턴스를 생성하는 경우 .NET 개체를 매개 변수로 생성자에게 제공하여 메시지의 본문으로 처리할 수 있습니다. AMQP 기본 형식으로 매핑할 수 있는 개체의 경우 본문은 AMQP 데이터 유형으로 직렬화됩니다. 개체를 AMQP 기본 형식으로 직접 매핑할 수 없는 경우 즉, 응용 프로그램에서 정의된 사용자 지정 형식이며 개체는 [DataContractSerializer][]를 사용하여 직렬화되고 직렬화된 바이트는 AMQP 데이터 메시지로 전송됩니다.

비 .NET 클라이언트와의 상호 운용성을 용이하게 하려면 메시지의 본문에 대한 AMQP 형식으로 직접 직렬화할 수 있는 .NET 형식만 사용합니다. 다음 표는 이러한 형식 및 AMQP 형식 시스템에 대한 해당 매핑을 자세히 설명합니다.

| .NET 본문 개체 형식 | 매핑된 AMQP 형식 | AMQP 본문 섹션 형식 |
|--------------------------------|-------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| bool | boolean | AMQP 값 |
| byte | ubyte | AMQP 값 |
| ushort | ushort | AMQP 값 |
| uint | uint | AMQP 값 |
| ulong | ulong | AMQP 값 |
| sbyte | byte | AMQP 값 |
| short | short | AMQP 값 |
| int | int | AMQP 값 |
| long | long | AMQP 값 |
| float | float | AMQP 값 |
| double | double | AMQP 값 |
| decimal | decimal128 | AMQP 값 |
| char | char | AMQP 값 |
| DateTime | timestamp | AMQP 값 |
| Guid | uuid | AMQP 값 |
| byte | binary | AMQP 값 |
| string | string | AMQP 값 |
| System.Collections.IList | list | AMQP 값: 컬렉션에 포함된 항목은 이 테이블에서 정의된 것만 가능합니다. |
| System.Array | array | AMQP 값: 컬렉션에 포함된 항목은 이 테이블에서 정의된 것만 가능합니다. |
| System.Collections.IDictionary | map | AMQP 값: 컬렉션에 포함된 항목은 이 테이블에서 정의된 것만 가능합니다.참고: 문자열만 지원됩니다. |
| Uri | 설명된 문자열(아래 표 참조) | AMQP 값 |
| DateTimeOffset | 설명된 long(아래 표 참조) | AMQP 값 |
| TimeSpan | 설명된 long(아래 참조) | AMQP 값 |
| Stream | binary | AMQP 데이터(여러 개가 있을 수 있음). 데이터 섹션에는 스트림 개체에서 읽은 원시 바이트가 포함되어 있습니다. |
| 다른 개체 | binary | AMQP 데이터(여러 개가 있을 수 있음). 응용 프로그램에서 제공된 DataContractSerializer 또는 serializer를 사용하는 개체의 직렬화된 이진을 포함합니다. |

| .NET 형식 | 매핑된 AMQP 설명된 형식 | 참고 |
|----------------|-------------------------------------------------------------------------------------------------------------------------|-------------------------|
| Uri | `<type name=”uri” class=restricted source=”string”> <descriptor name=”com.microsoft:uri” /></type>` | Uri.AbsoluteUri |
| DateTimeOffset | `<type name=”datetime-offset” class=restricted source=”long”> <descriptor name=”com.microsoft:datetime-offset” /></type>` | DateTimeOffset.UtcTicks |
| TimeSpan | `<type name=”timespan” class=restricted source=”long”> <descriptor name=”com.microsoft:timespan” /></type> ` | TimeSpan.Ticks |

## 지원되지 않는 기능, 제한 및 동작 차이

서비스 버스 .NET API의 다음 기능은 현재 AMQP 사용 시 지원되지 않습니다.

-   트랜잭션

-   전송 대상을 통해 보냅니다.

-   메시지 시퀀스 번호로 받습니다.

-   메시지 및 세션 탐색.

-   세션 상태.

-   일괄 처리 기반 API.

-   확장된 받기.

-   구독 규칙의 런타임 조작.

-   세션 잠금 갱신.

특히, 다음 API는 AMQP를 사용하는 경우 현재 지원되지 않습니다.

- [Microsoft.ServiceBus.Messaging.MessagingFactory.AcceptMessageSession][]
- [Microsoft.ServiceBus.Messaging.MessagingFactory.CreateMessageSender(System.String,System.String)][]

- [Microsoft.ServiceBus.Messaging.MessageSender.SendBatch(System.Collections.Generic.IEnumerable{Microsoft.ServiceBus.Messaging.BrokeredMessage})][]

- [Microsoft.ServiceBus.Messaging.MessageReceiver.Receive(System.Int64)][]
- [Microsoft.ServiceBus.Messaging.MessageReceiver.ReceiveBatch][]
- [Microsoft.ServiceBus.Messaging.MessageReceiver.CompleteBatch(System.Collections.Generic.IEnumerable{System.Guid})][]
- [Microsoft.ServiceBus.Messaging.MessageReceiver.Peek][]
- [Microsoft.ServiceBus.Messaging.MessageReceiver.PeekBatch][]

- [Microsoft.ServiceBus.Messaging.QueueClient.Peek][]
- [Microsoft.ServiceBus.Messaging.QueueClient.PeekBatch][]

- [Microsoft.ServiceBus.Messaging.TopicClient.SendBatch(System.Collections.Generic.IEnumerable{Microsoft.ServiceBus.Messaging.BrokeredMessage})][]

- [Microsoft.ServiceBus.Messaging.SubscriptionClient.Receive(System.Int64)][]
- [Microsoft.ServiceBus.Messaging.SubscriptionClient.ReceiveBatch][]
- [Microsoft.ServiceBus.Messaging.SubscriptionClient.CompleteBatch(System.Collections.Generic.IEnumerable{System.Guid})][]
- [Microsoft.ServiceBus.Messaging.SubscriptionClient.Peek][]
- [Microsoft.ServiceBus.Messaging.SubscriptionClient.PeekBatch][]
- [Microsoft.ServiceBus.Messaging.SubscriptionClient.AddRule][]
- [Microsoft.ServiceBus.Messaging.SubscriptionClient.RemoveRule(System.String)][]

- [Microsoft.ServiceBus.Messaging.MessageSession.GetState][]
- [Microsoft.ServiceBus.Messaging.MessageSession.SetState(System.IO.Stream)][]
- [Microsoft.ServiceBus.Messaging.MessageSession.RenewLock][]

- [Microsoft.ServiceBus.Messaging.BrokeredMessage.RenewLock][]

AMQP를 사용 하는 경우 기본 프로토콜에 비해 서비스 버스 .NET API의 동작에 몇 가지 작은 차이점이 있습니다.

-   [OperationTimeout][] 속성은 무시됩니다.

-   `MessageReceiver.Receive(TimeSpan.Zero)`은(는) `MessageReceiver.Receive(TimeSpan.FromSeconds(10))`(으)로 구현됩니다.

## AMQP 프로토콜 설정 제어

.NET API는 AMQP 프로토콜의 동작을 제어하기 위해 여러 설정을 노출합니다.

-   **MessageReceiver.PrefetchCount**: 링크에 적용되는 초기 크레딧을 제어합니다. 기본값은 0입니다.

-   **MessagingFactorySettings.AmqpTransportSettings.MaxFrameSize**: 연결 열기 시간 시 협상 동안 제공되는 최대 AMQP 프레임 크기를 제어합니다. 기본값은 65,536바이트입니다.

-   **MessagingFactorySettings.AmqpTransportSettings.BatchFlushInterval**: 전송을 배치로 사용 가능한 경우 이 값은 배치 전송을 위한 최대 지연을 결정합니다. 기본적으로 발신자/수신자를 상속합니다. 개별 발신자/수신자는 기본값 20 밀리초를 재정의할 수 있습니다.

-   **MessagingFactorySettings.AmqpTransportSettings.UseSslStreamSecurity**: AMQP 연결이 SSL 연결을 통해 설정되는지 여부를 제어합니다. 기본값은 **true**입니다.

## 다음 단계

자세히 알아볼 준비가 되셨습니까? 다음 링크를 방문하세요.

- [서비스 버스 AMQP 개요]
- [서비스 버스 분할 큐 및 항목을 위한 AMQP 1.0 지원]
- [Windows Server용 서비스 버스의 AMQP]

  [서비스 버스 큐를 사용하는 방법]: service-bus-dotnet-get-started-with-queues.md
  [DataContractSerializer]: https://msdn.microsoft.com/library/azure/system.runtime.serialization.datacontractserializer.aspx
  [BrokeredMessage]: https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.brokeredmessage.aspx
  [Microsoft.ServiceBus.Messaging.MessagingFactory.AcceptMessageSession]: https://msdn.microsoft.com/library/azure/jj657638.aspx
  [Microsoft.ServiceBus.Messaging.MessagingFactory.CreateMessageSender(System.String,System.String)]: https://msdn.microsoft.com/library/azure/jj657703.aspx
  [Microsoft.ServiceBus.Messaging.MessageSender.SendBatch(System.Collections.Generic.IEnumerable{Microsoft.ServiceBus.Messaging.BrokeredMessage})]: https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagesender.sendbatch.aspx
  [Microsoft.ServiceBus.Messaging.MessageReceiver.Receive(System.Int64)]: https://msdn.microsoft.com/library/azure/hh322665.aspx
  [Microsoft.ServiceBus.Messaging.MessageReceiver.ReceiveBatch]: https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagereceiver.receivebatch.aspx
  [Microsoft.ServiceBus.Messaging.MessageReceiver.CompleteBatch(System.Collections.Generic.IEnumerable{System.Guid})]: https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagereceiver.completebatch.aspx
  [Microsoft.ServiceBus.Messaging.MessageReceiver.Peek]: https://msdn.microsoft.com/library/azure/jj908731.aspx
  [Microsoft.ServiceBus.Messaging.MessageReceiver.PeekBatch]: https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagereceiver.peekbatch.aspx
  [Microsoft.ServiceBus.Messaging.QueueClient.Peek]: https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.peek.aspx
  [Microsoft.ServiceBus.Messaging.QueueClient.PeekBatch]: https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.peekbatch.aspx
  [Microsoft.ServiceBus.Messaging.TopicClient.SendBatch(System.Collections.Generic.IEnumerable{Microsoft.ServiceBus.Messaging.BrokeredMessage})]: https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.topicclient.sendbatch.aspx
  [Microsoft.ServiceBus.Messaging.SubscriptionClient.Receive(System.Int64)]: https://msdn.microsoft.com/library/azure/hh293110.aspx
  [Microsoft.ServiceBus.Messaging.SubscriptionClient.ReceiveBatch]: https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.subscriptionclient.receivebatch.aspx
  [Microsoft.ServiceBus.Messaging.SubscriptionClient.CompleteBatch(System.Collections.Generic.IEnumerable{System.Guid})]: https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.subscriptionclient.completebatch.aspx
  [Microsoft.ServiceBus.Messaging.SubscriptionClient.Peek]: https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.subscriptionclient.peek.aspx
  [Microsoft.ServiceBus.Messaging.SubscriptionClient.PeekBatch]: https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.subscriptionclient.peekbatch.aspx
  [Microsoft.ServiceBus.Messaging.SubscriptionClient.AddRule]: https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.subscriptionclient.addrule.aspx
  [Microsoft.ServiceBus.Messaging.SubscriptionClient.RemoveRule(System.String)]: https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.subscriptionclient.removerule.aspx
  [Microsoft.ServiceBus.Messaging.MessageSession.GetState]: https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagesession.getstate.aspx
  [Microsoft.ServiceBus.Messaging.MessageSession.SetState(System.IO.Stream)]: https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagesession.setstate.aspx
  [Microsoft.ServiceBus.Messaging.MessageSession.RenewLock]: https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagesession.renewlock.aspx
  [Microsoft.ServiceBus.Messaging.BrokeredMessage.RenewLock]: https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.brokeredmessage.renewlock.aspx
  [OperationTimeout]: https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx
[NuGet]: http://nuget.org/packages/WindowsAzure.ServiceBus/
[Azure 클래식 포털]: http://manage.windowsazure.com
[서비스 버스 AMQP 개요]: service-bus-amqp-overview.md
[서비스 버스 분할 큐 및 항목을 위한 AMQP 1.0 지원]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[Windows Server용 서비스 버스의 AMQP]: https://msdn.microsoft.com/library/dn574799.aspx

<!---HONumber=AcomDC_0608_2016-->