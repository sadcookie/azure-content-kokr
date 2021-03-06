<properties
	pageTitle="Azure 백업 자격 증명 모음 및 서버 관리 | Microsoft Azure"
	description="이 자습서를 사용하여 Azure 백업 저장소 및 서버를 관리하는 방법을 알아봅니다."
	services="backup"
	documentationCenter=""
	authors="Jim-Parker"
	manager="jwhit"
	editor="tysonn"/>

<tags
	ms.service="backup"
	ms.workload="storage-backup-recovery"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="04/01/2016"
	ms.author="jimpark;markgal"/>


# Azure 백업 자격 증명 모음 및 서버 관리
이 문서에서는 관리 포털 및 Microsoft Azure 백업 에이전트를 통해 사용할 수 있는 백업 관리 작업의 개요를 찾을 수 있습니다.

>[AZURE.NOTE] 이 문서에서는 클래식 배포 모델에서 작업하는 절차를 제공합니다.

## 관리 포털 작업
1. [관리 포털](https://manage.windowsazure.com)에 로그인합니다.

2. **복구 서비스**를 클릭한 후 백업 저장소의 이름을 클릭하여 빠른 시작 페이지를 표시합니다.

    ![Azure 백업 관리 탭](./media/backup-azure-manage-windows-server/rs-left-nav.png)

빠른 시작 페이지의 위쪽에 있는 옵션을 선택하여 사용 가능한 관리 작업을 볼 수 있습니다.

![Azure 백업 관리 탭](./media/backup-azure-manage-windows-server/qs-page.png)

### 대시보드
**대시보드**를 선택하여 서버의 사용 개요를 확인합니다. **사용 개요**에는 다음 정보가 포함됩니다.

- 클라우드에 등록된 Windows Server 수
- 클라우드에서 보호되는 Azure 가상 컴퓨터 수
- Azure에서 사용된 총 저장소
- 최근 작업의 상태

대시보드 아래쪽에서 수행할 수 있는 작업은 다음과 같습니다.

- **인증서 관리** - 서버를 등록하는 데 인증서가 사용된 경우 이 옵션을 통해 인증서를 업데이트합니다. 저장소 자격 증명을 사용하는 경우에는 **인증서 관리**를 사용해서는 안 됩니다.
- **삭제** - 현재 백업 저장소를 삭제합니다. 백업 자격 증명 모음이 더 이상 사용되지 않는 경우 삭제하여 저장소 공간을 확보할 수 있습니다. **삭제**는 등록된 모든 서버가 저장소에서 삭제된 후에만 사용할 수 있습니다.

![백업 대시보드 작업](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## 등록된 항목
**등록된 항목**을 선택하여 이 저장소에 등록된 서버의 이름을 표시합니다.

![등록된 항목](./media/backup-azure-manage-windows-server/registered-items.png)

**형식** 필터는 기본적으로 Azure 가상 컴퓨터로 설정됩니다. 이 자격 증명 모음에 등록된 서버의 이름을 확인하려면 드롭다운 메뉴에서 **Windows server**를 선택합니다.

여기서 다음 작업을 수행할 수 있습니다.

- **다시 등록 허용** - 서버에 이 옵션이 선택된 경우 온-프레미스 Microsoft Azure 백업 에이전트에서 **등록 마법사**를 사용하여 백업 저장소에 서버를 다시 등록할 수 있습니다. 인증서 오류로 인해 또는 서버를 다시 빌드해야 한 경우 다시 등록해야 할 수도 있습니다.
- **삭제** - 백업 저장소에서 서버를 삭제합니다. 서버와 관련해서 저장된 모든 데이터가 즉시 삭제됩니다.

    ![등록된 항목](./media/backup-azure-manage-windows-server/registered-items-tasks.png)

## 보호된 항목
**보호된 항목**을 선택하여 서버에서 백업된 항목을 표시합니다.

![보호된 항목](./media/backup-azure-manage-windows-server/protected-items.png)

## 구성

**구성** 탭에서 적절한 저장소 중복 옵션을 선택할 수 있습니다. 저장소 중복 옵션을 선택하기에 가장 좋은 시기는 자격 증명 모음을 만든 후 자격 증명 모음에 컴퓨터를 등록하기 바로 직전입니다.

>[AZURE.WARNING] 항목이 자격 증명 모음에 등록되고 나면 저장소 중복 옵션 잠기고 수정할 수 없습니다.

![구성](./media/backup-azure-manage-windows-server/configure.png)

[저장소 중복](../storage/storage-redundancy.md)에 대한 자세한 내용은 이 문서를 참조하세요.

## Microsoft Azure 백업 에이전트 작업

### 콘솔

**Microsoft Azure 백업 에이전트**를 엽니다(*Microsoft Azure 백업*에 대한 컴퓨터를 검색하여 찾을 수 있음).

![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/snap-in-search.png)

백업 에이전트 콘솔의 오른쪽에 있는 **작업**에서 다음 관리 작업을 수행할 수 있습니다.

- 서버 등록
- 백업 예약
- 지금 백업
- 속성 변경

![Microsoft Azure 백업 에이전트 콘솔 작업](./media/backup-azure-manage-windows-server/console-actions.png)

>[AZURE.NOTE] **데이터를 복구**하려면 [Windows 서버 또는 Windows 클라이언트 컴퓨터로 파일 복원](backup-azure-restore-windows-server.md)을 참조하세요.

### 기존 백업 수정

1. Microsoft Azure 백업 에이전트에서 **백업 예약**을 클릭합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/schedule-backup.png)

2. **백업 예약 마법사**에서 **백업 항목 또는 시간 변경** 옵션을 선택된 상태로 두고 **다음**을 클릭합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)

3. 항목을 추가하거나 변경하려면 **백업할 항목 선택** 화면에서 **항목 추가**를 클릭합니다.

    마법사의 이 페이지에서 **제외 설정**을 지정할 수도 있습니다. 파일 또는 파일 형식을 제외하려면 [제외 설정](#exclusion-settings) 추가 절차를 읽어보세요.

4. 백업할 파일 및 폴더를 선택하고 **확인**을 클릭합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/add-items-modify.png)

5. **백업 일정**을 지정하고 **다음**을 클릭합니다.

    매일(하루에 최대 3회) 또는 매주 백업을 예약할 수 있습니다.

    ![Windows Server 백업에 대한 항목](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

    >[AZURE.NOTE] 백업 일정을 지정하는 방법은 [문서](backup-azure-backup-cloud-as-tape.md)에 자세히 설명되어 있습니다.

6. 백업 복사본에 대한 **보존 정책**을 선택하고 **다음**을 클릭합니다.

    ![Windows Server 백업에 대한 항목](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)

7. **확인** 화면에서 정보를 검토하고 **마침**을 클릭합니다.

8. 마법사가 **백업 일정** 생성을 완료하면 **닫기**를 클릭합니다.

    보호를 수정한 후 **작업** 탭으로 이동해 변경 내용이 백업 작업에 반영되는지 확인하여 백업이 올바르게 트리거되는지 확인할 수 있습니다.

### 네트워크 제한 사용  
Azure 백업 에이전트는 데이터 전송 중에 네트워크 대역폭이 사용되는 방식을 제어할 수 있는 제한 탭을 제공합니다. 근무 시간에 데이터를 백업해야 하는데 백업 프로세스가 다른 인터넷 트래픽을 방해하지 말아야 할 때 유용한 기능입니다. 데이터 전송 제한은 백업 및 복원 작업에 적용됩니다.

제한을 사용하려면

1. **백업 에이전트**에서 **속성 변경**을 클릭합니다.

2. **백업 작업에 인터넷 대역폭 사용 제한 사용** 확인란을 선택합니다.

    ![네트워크 제한](./media/backup-azure-manage-windows-server/throttling-dialog.png)

3. 제한을 사용하도록 설정했으면 **근무 시간** 및 **휴무 시간** 중에 백업 데이터 전송에 허용되는 대역폭을 지정합니다.

    대역폭 값은 초당 512Kb(Kbps)에서 시작하여 최대 초당 1023Mb(Mbps)까지 증가할 수 있습니다. 또한 **근무 시간**의 시작 및 완료 시간과 근무일로 간주되는 요일을 지정할 수도 있습니다. 지정된 근무 시간 이외의 시간은 휴무 시간으로 간주됩니다.

4. **확인**을 클릭합니다.

## 제외 설정

1. **Microsoft Azure 백업 에이전트**를 엽니다(*Microsoft Azure 백업*에 대한 컴퓨터를 검색하여 찾을 수 있음).

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/snap-in-search.png)

2. Microsoft Azure 백업 에이전트에서 **백업 예약**을 클릭합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/schedule-backup.png)

3. 백업 예약 마법사에서 **백업 항목 또는 시간 변경** 옵션을 선택된 상태로 두고 **다음**을 클릭합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)

4. **제외 설정**을 클릭합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/exclusion-settings.png)

5. **제외 추가**를 클릭합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/add-exclusion.png)

6. 위치를 선택하고 **확인**을 클릭합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/exclusion-location.png)

7. **파일 형식** 필드에서 파일 확장명을 추가합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    .mp3 확장명 추가

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    다른 확장명을 추가하려면 **제외 추가**를 클릭하고 다른 파일 형식 확장명(.jpeg 확장명 추가)을 입력합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/exclude-jpg.png)

8. 모든 확장을 추가했으면 **확인**을 클릭합니다.

9. **확인 페이지**가 나타날 때까지 **다음**을 클릭하여 백업 예약 마법사를 계속 진행한 후 **마침**을 클릭합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## 다음 단계
- [Azure에서 Windows Server 또는 Windows 클라이언트 복원](backup-azure-restore-windows-server.md)
- Azure 백업에 대한 자세한 내용은 [Azure 백업 개요](backup-introduction-to-azure-backup.md)를 참조하세요.
- [Azure 백업 포럼](http://go.microsoft.com/fwlink/p/?LinkId=290933)을 방문하세요.

<!---HONumber=AcomDC_0413_2016-->