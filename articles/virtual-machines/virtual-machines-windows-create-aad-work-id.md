<properties
   pageTitle="AAD에서 회사 또는 학교 ID 만들기 | Microsoft Azure"
   description="Azure Active Directory에서 Windows 가상 컴퓨터로 사용할 회사 또는 학교 ID를 만드는 방법을 알아봅니다."
   services="virtual-machines-windows"
   documentationCenter=""
   authors="squillace"
   manager="timlt"
   editor=""
   tags="azure-service-management,azure-resource-manager"/>

<tags
   ms.service="virtual-machines-windows"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="vm-windows"
   ms.workload="infrastructure"
   ms.date="06/06/2016"
   ms.author="rasquill"/>

# Azure Active Directory에서 Windows VM으로 사용할 회사 또는 학교 ID 만들기

개인 Azure 계정을 생성하거나 개인 MSDN 구독이 있고 MSDN Azure 크레딧을 활용하기 위해 Azure 계정을 만든 경우는 *Microsoft 계정* ID를 사용하여 만든 것입니다. Azure의 많은 훌륭한 기능(예: [리소스 그룹 템플릿](../resource-group-overview.md))을 사용하기 위해서는 회사 또는 학교 계정(Azure Active Directory에서 관리하는 ID)이 필요합니다. 아래 지침을 따라 새로운 회사 또는 학교 계정을 만들 수 있는데 그 이유는 다행히 개인 Azure 계정이 제공하는 최고의 이점 중 하나는, 계정을 필요로 하는 Azure 기능과 함께 사용할 수 있는 새로운 회사 또는 학교 계정을 만드는 데 사용할 수 있는 기본 Azure Active Directory 도메인으로 제공된다는 점 때문입니다.

그러나 [여기](../xplat-cli-connect.md)에서 설명된 `azure login` 대화형 로그인 메서드를 사용하여 모든 유형의 Azure 계정으로 구독을 관리할 수 있도록 최근 변경되었습니다. 이 메커니즘을 사용하거나 또는 다음 지침을 따를 수 있습니다. [Azure Active Directory에서 Linux VM으로 사용할 회사 또는 학교 ID를 만들](virtual-machines-linux-create-aad-work-id.md) 수도 있습니다.

[AZURE.INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

[AZURE.INCLUDE [virtual-machines-common-create-aad-work-id](../../includes/virtual-machines-common-create-aad-work-id.md)]

<!---HONumber=AcomDC_0608_2016-->