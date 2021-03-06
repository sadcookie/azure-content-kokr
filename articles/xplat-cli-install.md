<properties
	pageTitle="Azure 명령줄 인터페이스 설치 | Microsoft Azure"
	description="Azure 서비스 사용을 시작하기 위해 Mac, Linux 및 Windows용 Azure 명령줄 인터페이스(Azure CLI) 설치 "
	editor=""
	manager="timlt"
	documentationCenter=""
	authors="dlepow"
	services="virtual-machines-linux,virtual-network,storage,azure-resource-manager"
	tags="azure-resource-manager,azure-service-management"/>

<tags
	ms.service="multiple"
	ms.workload="multiple"
	ms.tgt_pltfrm="command-line-interface"
	ms.devlang="na"
	ms.topic="article"
	ms.date="05/23/2016"
	ms.author="danlep"/>
    
# Azure CLI 설치

> [AZURE.SELECTOR]
- [PowerShell](powershell-install-configure.md)
- [Azure CLI](xplat-cli-install.md)

신속하게 Azure CLI(Azure 명령줄 인터페이스)를 설치하여 Microsoft Azure에서 리소스를 만들고 관리하기 위한 오픈 소스 셸 기반 명령 집합을 사용합니다. npm 패키지에서 설치하거나(Node.js 및 npm 필요), 서로 다른 운영 체제에 제공된 설치 관리자 패키지 중 하나를 사용하거나, Azure CLI를 Docker 호스트의 컨테이너로 설치하는 등 몇 가지 설치 옵션이 있습니다. 추가 옵션 및 배경 정보는 [GitHub](https://github.com/azure/azure-xplat-cli)에서 프로젝트 리포지토리를 참조하세요.


Azure CLI가 설치되었으면 [Azure 구독을 사용하여 연결](xplat-cli-connect.md)하고 명령줄 인터페이스(Bash, 터미널, 명령 프롬프트 등)에서 **azure** 명령을 실행하여 Azure 리소스 작업을 수행할 수 있습니다.



## npm 패키지 설치

npm 패키지에서 CLI를 설치하려면 최신 Node.js 및 npm이 시스템에 설치되어 있어야 합니다. 그러면 다음 명령을 실행하여 Azure CLI 패키지를 설치합니다. Linux 배포에서는 __npm__ 명령을 정상적으로 실행하기 위해 **sudo**를 사용해야 할 수도 있습니다.

	npm install azure-cli -g

> [AZURE.NOTE]운영 체제의 Node.js 및 npm을 설치하거나 업데이트해야 하는 경우 [Nodejs.org](https://nodejs.org/en/download/package-manager/)의 설명서를 참조하세요. 최신 Node.js LTS 버전(4.x)을 설치하는 것이 좋습니다. 이전 버전을 사용하는 경우 설치 오류가 발생할 수 있습니다.

## 설치 관리자 사용

다음과 같은 설치 관리자 패키지를 다운로드할 수도 있습니다.


* [OS X 설치 관리자][mac-installer]

* [Windows 설치 관리자][windows-installer]

* [Linux tar 파일][linux-installer](Node.js 및 npm 필요) - `sudo npm install -g <path to downloaded tar file>`를 실행하여 설치


## Docker 컨테이너 사용

Docker 호스트에서 다음을 실행합니다.

```
docker run -it microsoft/azure-cli
```

## Azure CLI 명령 실행
Azure CLI가 설치되었으면 명령줄 사용자 인터페이스(Bash, 터미널, 명령 프롬프트 등)에서 **azure** 명령을 실행할 수 있습니다. 예를 들어 help 명령을 실행하려면 다음을 입력합니다.

```
azure help
```
> [AZURE.NOTE]일부 Linux 배포에서 /usr/bin/env: ‘노드’: 그런 파일이나 디렉토리가 없습니다 오류가 발생할 수도 있으며, 이 오류는 /usr/bin/nodejs에 설치된 nodeJs의 최근 설치에서 비롯합니다. 이 오류를 해결하려면 아래 명령을 실행하여 /Usr/bin/node에 바로 가기 링크를 만듭니다.

```
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

설치한 Azure CLI의 버전을 보려면 다음을 입력합니다.

```
azure --version
```

이제 준비가 되었습니다! 사용자 고유의 리소스 작업을 수행하기 위해 모든 CLI 명령에 대한 액세스 권한을 얻으려면 [Azure CLI에서 Azure 구독에 연결](xplat-cli-connect.md)합니다.

>[AZURE.NOTE] Azure CLI 버전 0.9.20 또는 그 이상을 처음 사용할 때, 사용자가 CLI를 어떻게 사용하는지에 대한 정보를 Microsoft가 수집할 수 있도록 허용할 것인지 묻는 메시지가 표시됩니다. 참여는 자발적입니다. 참여하기로 선택한 경우, `azure telemetry --disable`을 실행하여 언제든지 중지할 수 있습니다. 언제라도 참여를 활성화하려면, `azure telemetry --enable`을 실행합니다.


## CLI 업데이트

Microsoft는 업데이트된 Azure CLI 버전을 자주 발표합니다. 운영 체제의 설치 관리자를 사용하여 CLI를 다시 설치하거나 최신 Node.js 및 npm이 설치된 경우 다음을 입력하여 업데이트합니다. Linux 배포에서는 **sudo**를 사용해야 할 수 있습니다.

```
npm update -g azure-cli
```

## 탭 완성 기능 사용

CLI 명령의 탭 완성 기능이 Mac 및 Linux에서 지원됩니다.

zsh에서 사용하도록 설정하려면 다음을 실행합니다.

```
echo '. <(azure --completion)' >> .zshrc
```

bash에서 사용하도록 설정하려면 다음을 실행합니다.

```
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## 다음 단계 

* [CLI에서 Azure 구독에 연결](xplat-cli-connect.md)하여 Azure 리소스를 만들고 관리합니다.

* Azure CLI에 대한 자세한 내용을 보거나, 소스 코드를 다운로드하거나, 문제를 보고하거나, 프로젝트에 기여하려면 [Azure CLI에 대한 GitHub 리포지토리](https://github.com/azure/azure-xplat-cli)를 방문하세요.

* Azure CLI 또는 Azure 사용에 대한 질문이 있는 경우 [Azure 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting)을 방문하세요.

* Linux 시스템의 경우 [소스](http://aka.ms/linux-azure-cli)에서 빌드하여 Azure CLI를 설치할 수도 있습니다. 원본에서 빌드하는 방법에 대한 자세한 내용은 원본 보관 파일에 포함된 INSTALL 파일을 참조하세요.

[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=windowsazurexplatcli&mode=new
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: virtual-machines-command-line-tools.md
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md

<!---HONumber=AcomDC_0629_2016-->