<properties 
	pageTitle="LOB(기간 업무) 응용 프로그램 4단계 | Microsoft Azure" 
	description="Azure의 LOB(기간 업무) 응용 프로그램의 4단계에서 웹 서버를 만들고 LOB(기간 업무) 응용 프로그램을 로드합니다." 
	documentationCenter=""
	services="virtual-machines-windows" 
	authors="JoeDavies-MSFT" 
	manager="timlt" 
	editor=""
	tags="azure-resource-manager"/>

<tags 
	ms.service="virtual-machines-windows" 
	ms.workload="infrastructure-services" 
	ms.tgt_pltfrm="vm-windows" 
	ms.devlang="na" 
	ms.topic="article" 
	ms.date="04/01/2016" 
	ms.author="josephd"/>

# LOB(기간 업무) 응용 프로그램 작업 4단계: 웹 서버 구성

Azure 인프라 서비스의 고가용성 LOB(기간 업무) 응용 프로그램을 배포하는 이 단계에서는 웹 서버를 구축하여 LOB 응용 프로그램을 로드합니다.

[5단계](virtual-machines-windows-ps-lob-ph5.md)로 진행하기 전에 이 단계를 완료해야 합니다. 모든 단계는 [Azure에서 고가용성 LOB(기간 업무) 응용 프로그램 배포](virtual-machines-windows-lob-overview.md)를 참조하세요.

## Azure에서 웹 서버 가상 컴퓨터 만들기

두 웹 서버 가상 컴퓨터에 ASP.NET 응용 프로그램 또는 Windows Server 2012 R2에서 IIS(Internet Information Services) 8이 호스팅할 수 있는 구형 응용 프로그램을 배포할 수 있습니다.

먼저 Azure가 두 웹 서버에서 클라이언트 트래픽을 LOB(기간 업무) 응용 프로그램에 균등하게 배분하도록 내부 부하 분산을 구성합니다. 이렇게 하려면 Azure 가상 네트워크에 할당한 서브넷 주소 공간으로부터 할당되는 자체 IP 주소와 이름으로 구성되는 내부 부하 분산 인스턴스를 지정해야 합니다.

> [AZURE.NOTE] 다음 명령 집합은 Azure PowerShell 1.0 이상을 사용합니다. 자세한 내용은 [Azure PowerShell 1.0](https://azure.microsoft.com/blog/azps-1-0/)을 참조하세요.

< and > 문자를 제거하고 변수의 값을 지정합니다. 다음 Azure PowerShell 명령 집합은 다음 표의 값을 사용합니다.

- 가상 컴퓨터의 경우 표 M
- 가상 네트워크 설정의 경우 표 V
- 서브넷의 경우 표 S
- 저장소 계정의 경우 표 ST
- 가용성 집합의 경우 표 A

[2단계](virtual-machines-windows-ps-lob-ph2.md)에서 정의한 테이블 M과, [1단계](virtual-machines-windows-ps-lob-ph1.md)에서 정의한 테이블 V, S, ST 및 A를 불러옵니다.

적절한 값을 모두 입력한 후 Azure PowerShell 명령 프롬프트에서 완성된 블록을 실행합니다.

	# Set up key variables
	$rgName="<resource group name>"
	$locName="<Azure location of your resource group>"
	$vnetName="<Table V – Item 1 – Value column>"
	$privIP="<available IP address on the subnet>"
	$vnet=Get-AzureRMVirtualNetwork -Name $vnetName -ResourceGroupName $rgName

	$frontendIP=New-AzureRMLoadBalancerFrontendIpConfig -Name WebServers-LBFE -PrivateIPAddress $privIP -SubnetId $vnet.Subnets[1].Id
	$beAddressPool=New-AzureRMLoadBalancerBackendAddressPoolConfig -Name WebServers-LBBE

	# This example assumes unsecured (HTTP-based) web traffic to the web servers.
	$healthProbe=New-AzureRMLoadBalancerProbeConfig -Name WebServersProbe -Protocol "TCP" -Port 80 -IntervalInSeconds 15 -ProbeCount 2
	$lbrule=New-AzureRMLoadBalancerRuleConfig -Name "WebTraffic" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol "TCP" -FrontendPort 80 -BackendPort 80
	New-AzureRMLoadBalancer -ResourceGroupName $rgName -Name "WebServersInAzure" -Location $locName -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe -FrontendIpConfiguration $frontendIP

다음으로 LOB(기간 업무) 응용 프로그램의 정규화된 도메인 이름(예: lobapp.corp.contoso.com)을 내부 부하 분산 장치에 할당된 IP 주소(앞의 Azure PowerShell 명령 블록에서 $privIP의 값)로 확인하는 DNS 주소 레코드를 조직 내부의 DNS 인프라에 추가합니다.

PowerShell 명령의 다음 블록을 사용하여 두 웹 서버용 가상 컴퓨터를 만듭니다.

적절한 값을 모두 입력한 후 Azure PowerShell 프롬프트에서 완성된 블록을 실행합니다.

	# Set up key variables
	$rgName="<resource group name>"
	$locName="<Azure location of your resource group>"
	$webLB=Get-AzureRMLoadBalancer -ResourceGroupName $rgName -Name "WebServersInAzure"	
	
	# Use the standard storage account
	$saName="<Table ST – Item 2 – Storage account name column>"

	$vnetName="<Table V – Item 1 – Value column>"
	$beSubnetName="<Table S - Item 2 - Name column>"
	$avName="<Table A – Item 3 – Availability set name column>"
	$vnet=Get-AzureRMVirtualNetwork -Name $vnetName -ResourceGroupName $rgName
	$backendSubnet=Get-AzureRMVirtualNetworkSubnetConfig -Name $beSubnetName -VirtualNetwork $vnet
	
	# Create the first web server virtual machine
	$vmName="<Table M – Item 6 - Virtual machine name column>"
	$vmSize="<Table M – Item 6 - Minimum size column>"
	$nic=New-AzureRMNetworkInterface -Name ($vmName + "-NIC") -ResourceGroupName $rgName -Location $locName -Subnet $backendSubnet -LoadBalancerBackendAddressPool $webLB.BackendAddressPools[0]
	$avSet=Get-AzureRMAvailabilitySet -Name $avName –ResourceGroupName $rgName 
	$vm=New-AzureRMVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avset.Id
	$cred=Get-Credential -Message "Type the name and password of the local administrator account for the first web server." 
	$vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
	$vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
	$vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
	$storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
	$osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/" + $vmName + "-OSDisk.vhd"
	$vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
	New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm
	
	# Create the second web server virtual machine
	$vmName="<Table M – Item 7 - Virtual machine name column>"
	$vmSize="<Table M – Item 7 - Minimum size column>"
	$nic=New-AzureRMNetworkInterface -Name ($vmName + "-NIC") -ResourceGroupName $rgName -Location $locName -Subnet $backendSubnet -LoadBalancerBackendAddressPool $webLB.BackendAddressPools[0]
	$vm=New-AzureRMVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avset.Id
	$cred=Get-Credential -Message "Type the name and password of the local administrator account for the second SQL Server computer." 
	$vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
	$vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
	$vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
	$storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
	$osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/" + $vmName + "-OSDisk.vhd"
	$vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
	New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

> [AZURE.NOTE] 이러한 가상 컴퓨터는 인트라넷 응용 프로그램용이므로 공용 IP 주소 또는 DNS 도메인 이름 레이블이 할당되지 않으며 인터넷에 노출되지 않습니다. 그러나 이는 Azure 포털에서도 연결할 수 없음을 의미합니다. 가상 컴퓨터의 속성을 볼 때 **연결** 단추를 사용할 수 없습니다.

원하는 원격 데스크톱 클라이언트를 사용하여 각 웹 서버 가상 컴퓨터에 대한 원격 데스크톱 연결을 만듭니다. 인트라넷 DNS 또는 컴퓨터 이름 및 로컬 관리자 계정의 자격 증명을 사용합니다.

다음으로 각 웹 서버 가상 컴퓨터에 대해 Windows PowerShell 프롬프트에서 다음 명령을 사용하여 적합한 Active Directory 도메인과 연결합니다.

	$domName="<Active Directory domain name to join, such as corp.contoso.com>"
	Add-Computer -DomainName $domName
	Restart-Computer

**Add-Computer** 명령을 입력한 후에는 반드시 도메인 계정 자격 증명을 제공해야 합니다.

다시 시작된 후 로컬 관리자 권한이 있는 계정을 사용하여 다시 연결합니다.

다음으로, 각 웹 서버에 대해 IIS를 설치 및 구성합니다.

1. 서버 관리자를 실행하고 **역할 및 기능 추가**를 클릭합니다.
2. 시작하기 전에 페이지에서 **다음**을 클릭합니다.
3. 설치 유형 선택 페이지에서 **다음**을 클릭합니다.
4. 대상 서버 선택 페이지에서 **다음**을 클릭합니다.
5. 서버 역할 페이지의 **역할** 목록에서 **웹 서버(IIS)**를 클릭합니다.
6. 메시지가 나타나면 **기능 추가**를 클릭하고 **다음**을 클릭합니다.
7. 기능 선택 페이지에서 **다음**을 클릭합니다.
8. 웹 서버(IIS) 페이지에서 **다음**을 클릭합니다.
9. 역할 서비스 선택 페이지에서 LOB 응용 프로그램에 필요한 서비스의 확인란을 선택하거나 선택 취소하고 **다음**을 클릭합니다. 10. 설치 선택 확인 페이지에서 **설치**를 클릭합니다.

## 웹 서버 가상 컴퓨터에서 LOB(기간 업무) 응용 프로그램을 배포합니다.

온-프레미스 네트워크에 있는 컴퓨터:

1.	두 웹 서버에 LOB(기간 업무) 응용 프로그램에 대한 파일을 추가합니다.
2.	SQL Server 클러스터에 LOB(기간 업무) 응용 프로그램에 대한 데이터베이스를 만듭니다.
3.	LOB(기간 업무) 응용 프로그램 및 그 기능에 대한 액세스를 테스트합니다.

이 단계를 올바르게 완료하면 이 표의 구성이 생성됩니다.

![](./media/virtual-machines-windows-ps-lob-ph4/workload-lobapp-phase4.png)

## 다음 단계

- [5단계](virtual-machines-windows-ps-lob-ph5.md)를 사용하여 이 워크로드의 구성을 완료합니다.

<!---HONumber=AcomDC_0601_2016-->