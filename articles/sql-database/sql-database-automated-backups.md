<properties
   pageTitle="클라우드 비즈니스 연속성 - 기본 제공 백업 - SQL 데이터베이스 | Microsoft Azure"
   description="Azure SQL 데이터베이스를 이전 지정 시간으로 롤백하거나 지리적 영역(최대 35일)의 새 데이터베이스에 데이터베이스를 복사할 수 있도록 하는 SQL 데이터베이스 기본 제공 백업에 대해 알아봅니다."
   services="sql-database"
   documentationCenter=""
   authors="carlrabeler"
   manager="jhubbard"
   editor="monicar"/>

<tags
   ms.service="sql-database"
   ms.devlang="NA"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="sqldb-bcdr"
   ms.date="06/16/2016"
   ms.author="carlrab"/>

# SQL 데이터베이스 자동화된 백업

Azure SQL 데이터베이스 서비스는 Basic의 경우 7일, Standard의 경우 14일 및 Premium의 경우 35일 동안 보존되는 자동화된 백업을 사용하여 모든 데이터베이스를 보호합니다. 각 서비스 계층에서 사용할 수 있는 기능에 대한 자세한 내용은 [서비스 계층](sql-database-service-tiers.md)을 참조하세요.

데이터베이스 백업은 옵트인할 필요나 추가 비용 없이 자동으로 수행됩니다. 이러한 자동화된 백업 및 특정 지점 복원은 실수로 손상 또는 삭제된 경우 원인이 무엇이든 데이터베이스를 보호하는 방법을 비용 및 관리 없이 제공합니다. 이러한 자동화된 백업을 사용하여 지정 시간 복원을 수행하고 데이터를 실수로 손상 또는 삭제한 후에 삭제된 데이터베이스를 복원할 수 있습니다.

## 자동화된 백업 비용

Microsoft Azure SQL 데이터베이스에서는 추가 비용 없이 최대 프로비전된 데이터베이스 저장소의 최대 200%까지 백업 저장소가 제공됩니다. 예를 들어, 프로비전된 DB의 크기가 250GB인 Standard DB 인스턴스가 있으면 추가 비용 없이 500GB의 백업 저장소가 제공됩니다. 데이터베이스가 제공된 백업 저장소를 초과하는 경우 Azure 지원에 문의하여 보존 기간을 줄이도록 선택하거나 표준 RA-GRS(읽기 액세스 지리 중복 저장소) 요금으로 청구되는 추가 백업 저장소에 대해 비용을 지불할 수 있습니다.

## 자동 백업 세부 정보

모든 기본, 표준 및 프리미엄 데이터베이스는 자동 백업에 의해 보호됩니다. 전체 백업은 매일, 차등 백업은 매주, 로그 백업은 5분 마다 수행됩니다. 첫 번째 전체 백업은 데이터베이스를 만든 후에 즉시 예약됩니다. 일반적으로 30분 이내에 완료되지만 더 오래 걸릴 수 있습니다. 예를 들어 데이터베이스가 이미 큰 경우, 큰 데이터베이스에서 데이터베이스를 복사 또는 복원하여 만들어진 경우 첫 번째 전체 백업은 완료하는 데 시간이 더 오래 걸릴 수 있습니다. 첫 번째 전체 백업 후에 모든 향후 백업은 자동으로 예약되며 백그라운드에서 자동으로 관리됩니다. 전체 및 차등 백업의 정확한 타이밍은 전체 부하를 분산하는 시스템에 의해 결정됩니다.

## 지리적 중복

백업 파일은 읽기 액세스 권한을 가진 지역 중복 저장소 계정(RA-GRS)에 저장되어 재해 복구에 대비한 가용성을 보장합니다. 다음에서는 읽기 액세스 권한을 가진 지역 중복 저장소 계정(RA-GRS)에 저장되어 재해 복구에 대비한 가용성을 보장하는 주간 및 일간 백업의 지역에서 복제를 보여 줍니다.

![geo-restore](./media/sql-database-geo-restore/geo-restore-1.png)

## 자동화된 백업 사용

[보존 기간](sql-database-service-tiers.md) 동안 [서비스에서 시작한 백업의 데이터베이스를](sql-database-recovery-using-backups.md) 다음으로 복원할 수 있습니다.

- 보존 기간 내에 지정된 지점으로 복구된 동일한 논리 서버의 새 데이터베이스
- 삭제된 데이터베이스에 대한 삭제 시간으로 복구된 동일한 논리 서버의 데이터베이스
- 지역에서 복제된 Blob 저장소(RA-GRS)의 최신 매일 백업으로 복구된 지역의 논리 서버에 있는 새 데이터베이스

[SQL 데이터베이스 자동화된 백업](sql-database-automated-backups.md)을 사용하여 현재 SQL 데이터베이스와 트랜잭션이 일치하는 지역의 논리 서버에서 [데이터베이스 복사본](sql-database-copy.md)을 만들 수도 있습니다. 데이터베이스 복사본을 사용하고 [BACPAC로 내보내](sql-database-export.md) 보존 기간 이상 장기간 저장하기 위해 트랜잭션이 일치하는 데이터베이스 복사본을 보관할 수도 있고, 온-프레미스 또는 SQL Server의 Azure VM 인스턴스로 데이터베이스 복사본을 전송할 수도 있습니다.

## 서비스 계층을 다운그레이드/업그레이드할 때 복원 지점 보존 기간은 어떻게 변경되나요?

낮은 성능 계층으로 다운그레이드 하면 복원 지점의 보존 기간은 현재 데이터베이스 성능 계층의 보존 기간으로 즉시 단축됩니다. 서비스 계층을 업그레이드 한 경우 보존 기간은 데이터베이스를 업그레이드한 후에만 확장이 시작됩니다. 예를 들어 데이터베이스가 P1에서 S3로 다운그레이드한 경우 보존 기간은 35일에서 14일로 즉시 변경되고, 14일 이전의 복원 지점을 더는 사용할 수 없게 됩니다. 이후에 다시 P1으로 업그레이드할 경우 보존 기간은 14일에서 시작하여 35일까지 작성되기 시작합니다.

## 삭제된 데이터베이스의 보존 기간은 얼마나 깁니까? 
보존 기간은 데이터베이스가 존재했던 서비스 계층 또는 데이터베이스 존재 일 수 중 더 적은 일 수에 의해 결정됩니다.

> [AZURE.IMPORTANT] Azure SQL 데이터베이스 서버 인스턴스를 삭제하면 모든 해당 데이터베이스도 삭제되고 복구할 수 없습니다. 현재는 삭제된 서버 복원에 대한 지원이 제공되지 않습니다.

## 다음 단계

- 복구를 위해 자동화된 백업을 사용하는 방법을 알아보려면 [서비스에서 시작한 백업에서 데이터베이스 복원](sql-database-recovery-using-backups.md)을 참조하세요.
- 빠른 복구 옵션에 대해 알아보려면 [활성 지역 복제](sql-database-geo-replication-overview.md)를 참조하세요.
- 보관을 위해 자동화된 백업을 사용하는 방법을 알아보려면 [데이터베이스 복사](sql-database-copy.md)를 참조하세요.
- 비즈니스 연속성을 대략적으로 이해하려면 [비즈니스 연속성 개요](sql-database-business-continuity.md)를 참조하세요.

<!---HONumber=AcomDC_0629_2016-->