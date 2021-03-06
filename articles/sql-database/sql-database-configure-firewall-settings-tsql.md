<properties
	pageTitle="T-SQL을 사용하는 Azure SQL 데이터베이스 서버 수준 및 데이터베이스 수준 방화벽 규칙 | Microsoft Azure"
	description="Azure SQL 데이터베이스에 액세스하는 IP 주소에 대한 방화벽을 구성하는 방법을 알아봅니다."
	services="sql-database"
	documentationCenter=""
	authors="BYHAM"
	manager="jhubbard"
	editor=""/>


<tags
	ms.service="sql-database"
	ms.workload="data-management"
	ms.tgt_pltfrm="na"
	ms.devlang="dotnet"
	ms.topic="article" 
	ms.date="06/15/2016"
	ms.author="rickbyh"/>


# T-SQL을 사용하여 Azure SQL 데이터베이스 서버 수준 및 데이터베이스 수준 방화벽 규칙 구성


> [AZURE.SELECTOR]
- [개요](sql-database-firewall-configure.md)
- [Azure 포털](sql-database-configure-firewall-settings.md)
- [TSQL](sql-database-configure-firewall-settings-tsql.md)
- [PowerShell](sql-database-configure-firewall-settings-powershell.md)
- [REST API](sql-database-configure-firewall-settings-rest.md)


Microsoft Azure SQL 데이터베이스 서버와 데이터베이스에 대한 연결을 허용 하도록 방화벽 규칙을 사용 합니다. 선택적으로 데이터베이스에 대한 액세스를 허용 하도록 Azure SQL 데이터베이스 서버에서 master 데이터베이스 또는 사용자 데이터베이스에 대한 서버 수준 및 데이터베이스 수준 방화벽 설정을 정의할 수 있습니다.

> [AZURE.IMPORTANT] Azure에서 응용 프로그램 데이터베이스 서버에 연결할 수 있게 하려면 Azure 연결을 사용하도록 설정해야 합니다. 방화벽 규칙 및 Azure의 연결을 사용하도록 설정 하는 방법에 대한 자세한 내용은 [Azure SQL 데이터베이스 방화벽](sql-database-firewall-configure.md)을 참조하세요. Azure 클라우드 경계 내에서 연결하는 경우 일부 TCP 포트를 추가로 열어야 할 수도 있습니다. 자세한 내용은 [ADO.NET 4.5 및 SQL 데이터베이스 V12에 대한 1433 이외의 포트](sql-database-develop-direct-route-ports-adonet-v12.md)의 **SQL 데이터베이스의 V12: 내부 vs 외부** 섹션을 참조하세요.


## Transact-SQL을 통해 서버 수준 방화벽 규칙 관리

서버 수준 보안 주체 로그인 또는 Azure Active Directory 관리자만이 Transact-SQL을 사용하여 서버 수준 방화벽 규칙을 만들 수 있습니다.

1. SQL Server Management Studio를 사용하여 쿼리 창을 시작하고 가상 마스터 데이터베이스에 연결합니다.
2. 서버 수준 방화벽 규칙은 쿼리 창 내에서 선택, 생성, 업데이트 또는 삭제할 수 있습니다.
3. 0서버 수준 방화벽 규칙을 만들거나 업데이트 하려면 sp\_set\_firewall 규칙 저장 프로시저를 실행 합니다. 다음 예제는 Contoso 서버에서 일정 범위의 IP 주소를 사용하도록 설정합니다.<br/>먼저 이미 존재하는 규칙을 확인합니다.

		SELECT * FROM sys.firewall_rules ORDER BY name;

	그런 다음 방화벽 규칙을 추가합니다.

		EXECUTE sp_set_firewall_rule @name = N'ContosoFirewallRule',
			@start_ip_address = '192.168.1.1', @end_ip_address = '192.168.1.10'

	서버 수준 방화벽 규칙을 삭제 하려면 sp\_delete\_firewall\_rule 저장 프로시저를 실행 합니다. 다음 예제에서는 ContosoFirewallRule 이라는 규칙을 삭제 합니다.
 
		EXECUTE sp_delete_firewall_rule @name = N'ContosoFirewallRule'
 
 이러한 저장 프로시저에 대한 자세한 내용은 [sp\_set\_firewall\_rule](https://msdn.microsoft.com/library/dn270017.aspx) 및 [sp\_delete\_firewall\_rule](https://msdn.microsoft.com/library/dn270024.aspx)을 참조하세요.

## 데이터베이스 수준 방화벽 규칙

데이터베이스에 대한 **제어** 권한이 있는 데이터베이스 사용자(예: 데이터베이스 소유자)만이 데이터베이스 수준 방화벽 규칙을 만들 수 있습니다.

1. 사용자의 IP 주소에 대한 서버 수준 방화벽을 만든 후 클래식 포털 또는 SQL Server Management Studio를 통해 쿼리 창을 시작합니다.
2. 데이터베이스 수준 방화벽 규칙을 만들려는 데이터베이스에 연결 합니다.

	기존 데이터베이스 수준 방화벽 규칙을 새로 만들거나 업데이트 하려면 sp\_set\_database\_firewall\_rule 저장 프로시저를 실행 합니다. 다음 예제에서는 ContosoFirewallRule 이라는 새 방화벽 규칙을 만듭니다.
 
		EXEC sp_set_database_firewall_rule @name = N'ContosoFirewallRule', 
		    @start_ip_address = '192.168.1.11', @end_ip_address = '192.168.1.11'
 
	기존 데이터베이스 수준 방화벽 규칙을 삭제 하려면 sp\_delete\_database\_firewall\_rule 저장 프로시저를 실행 합니다. 다음 예제에서는 ContosoFirewallRule 이라는 규칙을 삭제 합니다.
 
		EXEC sp_delete_database_firewall_rule @name = N'ContosoFirewallRule'

이러한 저장 프로시저에 대한 자세한 내용은 [sp\_set\_database\_firewall\_rule](https://msdn.microsoft.com/library/dn270010.aspx) 및 [sp\_delete\_database\_firewall\_rule](https://msdn.microsoft.com/library/dn270030.aspx)을 참조하세요.

## 다음 단계

다른 방법을 사용한 서버 수준 방화벽 규칙 만들기에 대한 방법 문서를 보려면 다음을 참조하세요.

- [Azure 포털을 사용하여 Azure SQL 데이터베이스 서버 수준 방화벽 규칙 구성](sql-database-configure-firewall-settings.md)
- [PowerShell을 사용하여 Azure SQL 데이터베이스 서버 수준 방화벽 규칙 구성](sql-database-configure-firewall-settings-powershell.md)
- [REST API를 사용하여 Azure SQL 데이터베이스 서버 수준 방화벽 규칙 구성](sql-database-configure-firewall-settings-rest.md)

데이터베이스를 만드는 방법에 대한 자습서는 [Azure 포털을 사용하여 빠르게 SQL 데이터베이스 만들기](sql-database-get-started.md)를 참조하세요. 오픈 소스 또는 타사 응용 프로그램에서 Azure SQL 데이터베이스에 연결하는 방법에 대한 도움말은 [SQL 데이터베이스에 대한 클라이언트 빠른 시작 코드 샘플](https://msdn.microsoft.com/library/azure/ee336282.aspx)을 참조하세요. 데이터베이스를 탐색하는 방법을 이해하려면 [데이터베이스 및 로그인 보안 관리](https://msdn.microsoft.com/library/azure/ee336235.aspx)를 참조하세요.


## 추가 리소스

- [데이터베이스 보안 설정](sql-database-security.md)
- [SQL Server 데이터베이스 엔진 및 Azure SQL 데이터베이스 보안 센터](https://msdn.microsoft.com/library/bb510589)

<!---HONumber=AcomDC_0622_2016-->