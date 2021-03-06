<properties
        pageTitle="CLI에서 Linux VM 암호 및 SSH 키 재설정 | Microsoft Azure"
        description="Azure 명령줄 인터페이스(CLI)에서 VMAccess 확장을 사용하여 Linux VM 암호 또는 SSH 키 재설정, SSH 구성 수정, 디스크 일관성 검사를 수행하는 방법"
        services="virtual-machines-linux"
        documentationCenter=""
        authors="cynthn"
        manager="timlt"
        editor=""
        tags="azure-service-management"/>

<tags
        ms.service="virtual-machines-linux"
        ms.workload="infrastructure-services"
        ms.tgt_pltfrm="vm-linux"
        ms.devlang="na"
        ms.topic="article"
        ms.date="06/14/2016"
        ms.author="cynthn"/>

# VMAccess 확장을 사용하여 Linux VM 암호 또는 SSH 키 재설정, SSH 구성 수정, 디스크 일관성 검사를 수행하는 방법


암호를 잊었거나 SSH(보안 셸) 키가 맞지 않거나 SSH 구성에 문제가 생겨서 Azure에서 Linux 가상 컴퓨터에 연결할 수 없는 경우 VMAccessForLinux 확장과 Azure CLI를 사용하여 암호 또는 SSH 키를 재설정하고 SSH 구성을 수정하며 디스크 일관성을 검사합니다.

[AZURE.INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-classic-include.md)] [Resource Manager 모델을 사용하여 이러한 단계를 수행](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess)하는 방법을 알아봅니다.

Azure CLI에서는 명령줄 인터페이스(Bash, 터미널, 명령 프롬프트)에서 **azure vm extension set** 명령을 사용하여 명령에 액세스할 수 있습니다. 자세한 확장 사용을 보려면 **azure help vm extension set**를 실행합니다.

Azure CLI를 사용하여, 다음 작업을 수행할 수 있습니다.

+ [암호 재설정](#pwresetcli)
+ [SSH 키 재설정](#sshkeyresetcli)
+ [암호 및 SSH 키 재설정](#resetbothcli)
+ [새 sudo 사용자 계정 만들기](#createnewsudocli)
+ [SSH 구성 재설정](#sshconfigresetcli)
+ [사용자 삭제](#deletecli)
+ [VMAccess 확장 상태 표시](#statuscli)
+ [추가된 디스크의 일관성 검사](#checkdisk)
+ [Linux VM에서 추가된 디스크 복구](#repairdisk)


## 필수 조건

다음을 수행해야 합니다.

- 계정과 연결된 Azure 리소스를 사용하려면 [Azure CLI를 설치](../xplat-cli-install.md)하고 [구독에 연결](../xplat-cli-connect.md)해야 합니다.
- 명령 프롬프트에서 다음을 입력하여 클래식 배포 모델에 대한 올바른 모드를 설정합니다.
        
        azure config mode asm
        
- 새 암호 또는 SSH 키 집합(둘 중 하나를 다시 설정하려는 경우). SSH 구성을 다시 설정하려는 경우에는 필요 없습니다.


## <a name="pwresetcli"></a>암호 재설정

1. 다음 줄을 사용하여 PrivateConf.json이라는 파일을 만듭니다. 대괄호 및 &#60;자리 표시자&#62; 값을 사용자의 정보로 바꿉니다.

        {
        "username":"<currentusername>",
        "password":"<newpassword>",
        "expiration":"<2016-01-01>"
        }

2. 이 명령을 실행하여 &#60;vm-name&#62;에 대한 가상 컴퓨터의 이름을 대체합니다

        azure vm extension set <vm-name> VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json

## <a name="sshkeyresetcli"></a>SSH 키 재설정

1. 이 콘텐츠를 포함한 PrivateConf.json이라는 파일을 만듭니다. 대괄호 및 &#60;자리 표시자&#62; 값을 사용자의 정보로 바꿉니다.

        {
        "username":"<currentusername>",
        "ssh_key":"<contentofsshkey>"
        }

2. 이 명령을 실행하여 &#60;vm-name&#62;에 대한 가상 컴퓨터의 이름을 대체합니다

        azure vm extension set <vm-name> VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <a name="resetbothcli"></a>암호 및 SSH 키 재설정

1. 이 콘텐츠를 포함한 PrivateConf.json이라는 파일을 만듭니다. 대괄호 및 &#60;자리 표시자&#62; 값을 사용자의 정보로 바꿉니다.

        {
        "username":"<currentusername>",
        "ssh_key":"<contentofsshkey>",
        "password":"<newpassword>"
        }

2. 이 명령을 실행하여 &#60;vm-name&#62;에 대한 가상 컴퓨터의 이름을 대체합니다

        azure vm extension set <vm-name> VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <a name="createnewsudocli"></a>새 sudo 사용자 계정 만들기

사용자 이름을 잊은 경우 sudo 기관으로 새 레코드를 만들려면 VMAccess를 사용할 수 있습니다. 이 경우 기존 사용자 이름 및 암호는 수정되지 않습니다.

암호 액세스가 있는 새 sudo 사용자를 만들려면, [암호 재설정](#pwresetcli)에서 스크립트를 사용하여 새 사용자 이름을 지정합니다.

SSH 키 액세스가 있는 새 sudo 사용자를 만들려면, [SSH 키 재설정](#sshkeyresetcli)에서 스크립트를 사용하여 새 사용자 이름을 지정합니다.

[암호 및 SSH 키 재설정](#resetbothcli)을 사용하여 암호 및 SSH 키 액세스 모두가 있는 새 사용자를 만듭니다.

## <a name="sshconfigresetcli"></a>SSH 구성 재설정

SSH 구성이 원치 않는 상태인 경우, VM에 대한 액세스도 손실될 수 있습니다. 구성을 기본 상태로 다시 설정하려면 VMAccess 확장을 사용할 수 있습니다. 이렇게 하려면 "reset\_ssh" 키를 "True"로 설정하기만 하면 됩니다. 확장에서 SSH 서버를 다시 시작하고, VM에서 SSH 포트를 연 다음, SSH 구성을 기본값으로 다시 설정합니다. 사용자 계정(이름, 암호 또는 SSH 키)은 변경되지 않습니다.

> [AZURE.NOTE] 재설정된 SSH 구성 파일은 /etc/ssh/sshd\_config에 있습니다.

1. 이 콘텐츠를 포함한 PrivateConf.json이라는 파일을 만듭니다.

        {
        "reset_ssh":"True"
        }

2. 이 명령을 실행하여 &#60;vm-name&#62;에 대한 가상 컴퓨터의 이름을 대체합니다

        azure vm extension set <vm-name> VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <a name="deletecli"></a>사용자 삭제

VM에 직접 로그인하지 않고 사용자 계정을 삭제하려면 이 스크립트를 사용합니다.

1. 이 콘텐츠를 사용하고 &#60;usernametoremove&#62;에 제거할 사용자 이름을 지정하여 PrivateConf.json이라는 파일을 만듭니다.

        {
        "remove_user":"<usernametoremove>"
        }

2. 이 명령을 실행하여 &#60;vm-name&#62;에 대한 가상 컴퓨터의 이름을 대체합니다

        azure vm extension set <vm-name> VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <a name="statuscli"></a>VMAccess 확장 상태 표시

VMAccess 확장 상태를 표시하려면, 다음 명령을 실행합니다.

        azure vm extension get

## <a name='checkdisk'<</a>추가된 디스크의 일관성 검사

Linux 가상 컴퓨터의 모든 디스크에 fsck를 실행하려면, 다음을 수행해야 합니다.

1. 이 콘텐츠를 포함하는 PublicConf.json 파일을 만듭니다. 디스크 검사는 부울 함수를 통해 가상 컴퓨터에 연결되어 있는 디스크를 검사할지 여부를 결정합니다.

        {   
        "check_disk": "true"
        }

2. &#60;vm-name&#62;에 가상 컴퓨터 이름을 지정하여 이 명령을 실행합니다.

        azure vm extension set <vm-name> VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 

## <a name='repairdisk'></a>디스크 복구 

탑재가 되지 않거나 탑재 구성 오류가 있는 디스크를 복구하려면, VMAccess 확장을 사용하여 Linux 가상 컴퓨터의 탑재 구성을 재설정합니다. &#60;yourdisk&#62;에 디스크 이름을 입력합니다.

1. 이 콘텐츠를 포함하는 PublicConf.json 파일을 만듭니다.

        {
        "repair_disk":"true",
        "disk_name":"<yourdisk>"
        }

2. &#60;vm-name&#62;에 가상 컴퓨터 이름을 지정하여 이 명령을 실행합니다.

        azure vm extension set <vm-name> VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json



## 다음 단계

* Azure PowerShell cmdlet 또는 Azure Resource Manager 템플릿을 사용하여 암호 또는 SSH 키 재설정, SSH 구성 수정, 디스크 일관성 검사를 수행하려면 [GitHub의 VMAccess 확장 문서](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess)를 참조하세요.

* 또한 [Azure 포털](https://portal.azure.com)을 사용하여 클래식 배포 모델에서 배포된 Linux VM의 암호 또는 SSH 키를 재설정할 수 있습니다. 현재는 이 포털을 사용하여 Resource Manager 배포 모델에 배포된 Linux VM에 대해 이 작업을 수행할 수 없습니다.

* Azure 가상 컴퓨터에 VM 확장을 사용하는 방법에 대한 자세한 내용은 [가상 컴퓨터 확장 및 기능 정보](virtual-machines-linux-extensions-features.md)를 참조하세요.

<!---HONumber=AcomDC_0629_2016-->