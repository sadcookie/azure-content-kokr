## 역방향 DNS 레코드란 무엇인가요?

역방향 DNS 레코드는 다양한 상황에 사용됩니다. 서버 유효성 검사 및 요청 중 서버 요청을 인증합니다. 예를 들어 역방향 DNS 레코드는 보낸 사람의 메일 메시지를 확인하여 스팸 메일을 방지하는 데 널리 사용됩니다. 그 과정에서 역방향 DNS 레코드를 확인하고, 해당 호스트가 원래의 도메인에서 메일을 보내도록 허가를 받은 것으로 인식되었는지도 확인합니다.<BR> 역방향 DNS 레코드 또는 PTR 레코드는 공개적으로 라우트 가능한 IP 주소를 이름으로 다시 변환할 수 있는 DNS 레코드 유형입니다. DNS에서 app1.contoso.com과 같은 이름은 정방향 확인이라고 하는 프로세스에서 IP 주소로 확인됩니다. 역방향 DNS를 사용하면 이 프로세스가 해당 IP 주소가 지정된 이름 확인을 반대로 진행합니다.<BR> 역방향 DNS 레코드에 대한 자세한 내용은 [여기](http://en.wikipedia.org/wiki/Reverse_DNS_lookup)를 참조하세요.<BR>

## Azure에서는 Azure 서비스에 대해 역방향 DNS 레코드를 어떻게 지원하나요?

Microsoft는 다양한 레지스트리를 사용하여 공개적으로 라우트 가능한 IP 블록의 적합한 제공을 보호합니다. 그러면 이러한 각 블록이 Microsoft가 소유하고 운영하는 신뢰할 수 있는 DNS 서버로 위임됩니다. Microsoft는 할당된 공개적으로 라우트 가능한 모든 IP 블록에 대한 역방향 DNS 영역을 호스트합니다. <BR> Azure는 배포에 할당된 공개적으로 라우트 가능한 IP의 사용자 지정 FQDN(정규화된 도메인 이름)을 지정할 수 있습니다. 그러면 이러한 사용자 지정 FQDN이 해당 IP의 역방향 DNS 조회에 대해 반환됩니다.<BR> Azure는 추가 비용 없이 공개적으로 라우트 가능한 모든 IP와 클래식 및 ARM 배포 모델을 사용하여 배포된 서비스에 대해 역방향 DNS 지원을 제공합니다.

<!---HONumber=AcomDC_0316_2016-->