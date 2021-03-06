---
title: 백업에서 Azure SQL Database 복원 | Microsoft Docs
description: Azure SQL Database를 이전 시점(최대 35일)에 롤백할 수 있는 특정 시점 복원에 대해 알아봅니다.
services: sql-database
ms.service: sql-database
ms.subservice: backup-restore
ms.custom: ''
ms.devlang: ''
ms.topic: conceptual
author: anosov1960
ms.author: sashan
ms.reviewer: mathoma, carlrab
manager: craigg
ms.date: 03/12/2019
ms.openlocfilehash: ca54ae11390b388c3158bd220ee5c7829172a5c3
ms.sourcegitcommit: f8c592ebaad4a5fc45710dadc0e5c4480d122d6f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58620481"
---
# <a name="recover-an-azure-sql-database-using-automated-database-backups"></a>자동화된 데이터베이스 백업을 사용하여 Azure SQL 데이터베이스 복구

기본적으로 SQL Database 백업은 지역 복제 Blob Storage(RA-GRS)에 저장됩니다. 다음 옵션은 [자동화된 데이터베이스 백업](sql-database-automated-backups.md)을 통한 데이터베이스 복구에 사용할 수 있습니다.

- 동일한 SQL Database 서버에 보존 기간 내의 지정된 시점으로 복구된 새 데이터베이스를 만듭니다.
- 동일한 SQL Database 서버에 삭제된 데이터베이스의 삭제 시간으로 복구된 데이터베이스를 만듭니다.
- 동일한 지역의 임의 SQL Database 서버에 최신 백업 지점으로 복구된 새 데이터베이스를 만듭니다.
- 다른 지역의 임의 SQL Database 서버에 최신 복제 백업 지점으로 복구된 새 데이터베이스를 만듭니다.

[백업 장기 보존](sql-database-long-term-retention.md)을 구성한 경우 임의 지역의 임의 SQL Database 서버에 있는 임의 LTR 백업에서 새 데이터베이스를 만들 수도 있습니다.

> [!IMPORTANT]
> 복원하는 동안 기존 데이터베이스를 덮어쓸 수는 없습니다.

표준 또는 프리미엄 서비스 계층을 사용하는 경우 다음 조건에 따라 복원된 데이터베이스에서 추가 저장소 비용이 발생합니다.

- 데이터베이스 최대 크기가 500GB보다 큰 경우 P11–P15에서 S4-S12 또는 P1–P6로의 복원
- 데이터베이스 최대 크기가 250GB보다 큰 경우 P1–P6에서 S4-S12로의 복원

추가 비용은 복원된 데이터베이스의 최대 크기가 계산 크기에 대해 포함된 저장소의 크기보다 크고, 포함된 크기 이상으로 프로비전된 추가 저장소에는 추가 요금이 부과되기 때문에 발생합니다. 추가 저장소에 대한 가격 책정 정보는 [SQL Database 가격 책정 페이지](https://azure.microsoft.com/pricing/details/sql-database/)를 참조하세요. 실제 사용된 공간의 크기가 포함된 저장소의 크기보다 작은 경우 데이터베이스 최대 크기를 포함된 크기로 줄여 이러한 추가 비용을 방지할 수 있습니다.

> [!NOTE]
> [데이터베이스 사본](sql-database-copy.md)을 만들 때 [자동화된 데이터베이스 백업](sql-database-automated-backups.md)이 사용됩니다.

## <a name="recovery-time"></a>복구 시간

자동화된 데이터베이스 백업을 사용하여 데이터베이스를 복원하기 위한 복구 시간은 다음과 같은 다양한 요인의 영향을 받습니다.

- 데이터베이스의 크기
- 데이터베이스의 계산 크기
- 관련된 트랜잭션 로그의 수
- 복원 지점으로 복구하기 위해 재생해야 하는 작업의 양
- 다른 지역으로 복원되는 경우의 네트워크 대역폭
- 대상 지역에서 처리되는 동시 복원 요청 개수

매우 큰 및/또는 활성 데이터베이스의 경우 복원에는 몇 시간이 걸릴 수 있습니다. 지역에서 장시간 가동 중단된 경우 다른 지역에서 많은 수의 지리적 복원 요청이 처리 중일 수 있습니다. 많은 요청이 있는 경우 해당 지역에 데이터베이스의 복구 시간이 늘어날 수 있습니다. 대부분의 데이터베이스는 12시간 내에 완전히 복원됩니다.

단일 구독의 경우 제출되고 계속 진행되는 동시 복원 요청 수에 대해 몇 가지 제한 사항(예: 지정 시간 복원, 지역 복원, 장기 보존 백업에서 복원)이 있습니다.

| | **처리되는 최대 동시 요청 수** | **제출되는 최대 동시 요청 수** |
| :--- | --: | --: |
|단일 데이터베이스(구독당)|10|60|
|탄력적 풀(풀당)|4|200|
||||

대량 복원을 위한 기본 제공 기능은 없습니다. [Azure SQL Database: Full Server Recovery](https://gallery.technet.microsoft.com/Azure-SQL-Database-Full-82941666) 스크립트는 이 작업을 수행하는 한 가지 방법의 예입니다.

> [!IMPORTANT]
> 자동화된 백업을 사용하여 복구하려면 구독에서 SQL Server 참여자 역할의 구성원이거나 구독 소유자여야 합니다. [RBAC: 기본 제공 역할](../role-based-access-control/built-in-roles.md)을 참조하세요. Azure 포털, PowerShell 또는 REST API를 사용하여 복구할 수 있습니다. Transact-SQL은 사용할 수 없습니다.

## <a name="point-in-time-restore"></a>지정 시간 복원

Azure Portal, [PowerShell](https://docs.microsoft.com/powershell/module/az.sql/restore-azsqldatabase) 또는 [REST API](https://docs.microsoft.com/rest/api/sql/databases)를 사용하여 동일한 서버에 독립 실행형 데이터베이스, 풀링된 데이터베이스 또는 인스턴스 데이터베이스를 새 데이터베이스로써 이전 시점으로 복원할 수 있습니다. 데이터베이스를 원하는 서비스 계층 또는 계산 크기로 복원할 수 있습니다. 서버에 데이터베이스를 복원하기에 충분한 리소스가 있는지 확인합니다. 완료되면 복원된 데이터베이스는 일반적이고 완벽하게 액세스할 수 있는 온라인 데이터베이스입니다. 복원된 데이터베이스는 서비스 계층 및 계산 크기에 따라 정상 요금이 청구됩니다. 데이터베이스 복원이 완료될 때까지 요금이 발생하지 않습니다.

일반적으로 복구를 위해 이전 지점까지 데이터베이스를 복원합니다. 이렇게 하는 경우 원본 데이터베이스에 대한 대체로 복원된 데이터베이스를 처리하거나 데이터를 검색하고 원래 데이터베이스를 업데이트하는 데 사용할 수 있습니다.

- **데이터베이스 교체**

  복원된 데이터베이스를 원래 데이터베이스에 대한 대체로 여기는 경우 계산 크기 및 서비스 계층이 적절한지 확인하고 필요한 경우 데이터베이스의 크기를 조정해야 합니다. 원본 데이터베이스의 이름을 바꿀 수 있으며 T-SQL에서 [ALTER DATABASE](/sql/t-sql/statements/alter-database-azure-sql-database) 명령을 사용하여 복원된 데이터베이스에 원래 이름을 제공할 수 있습니다.

- **데이터 복구**

  복원된 데이터베이스에서 데이터를 가져와 사용자 또는 애플리케이션 오류로부터 복구하려면 복원된 데이터베이스에서 원본 데이터베이스로 데이터를 추출하는 데 필요한 데이터 복구 스크립트를 작성하고 실행해야 합니다. 복원 작업을 완료하는 데 긴 시간이 걸리지만 복원 중인 데이터베이스가 복원 과정 내내 데이터베이스 목록에 표시됩니다. 복원하는 동안 데이터베이스를 삭제하는 경우 작업이 취소되고 복원이 완료되지 않은 데이터베이스에 대해서는 비용이 청구되지 않습니다.

Azure Portal을 사용하여 단일 데이터베이스, 풀링된 데이터베이스 또는 인스턴스 데이터베이스를 특정 시점으로 복구하려면 데이터베이스에 대한 페이지를 열고 도구 모음에서 **복원**을 클릭합니다.

![point-in-time-restore](./media/sql-database-recovery-using-backups/point-in-time-recovery.png)

> [!IMPORTANT]
> 프로그래밍 방식으로 백업에서 데이터베이스를 복원하려면 [자동화된 백업을 사용하여 프로그래밍 방식으로 복구 수행](sql-database-recovery-using-backups.md#programmatically-performing-recovery-using-automated-backups)을 참조하세요.

## <a name="deleted-database-restore"></a>삭제된 데이터베이스 복원

삭제된 데이터베이스 복원을 사용하면 Azure Portal, [PowerShell](https://docs.microsoft.com/powershell/module/az.sql/restore-azsqldatabase) 또는 [REST(createMode=Restore)](https://docs.microsoft.com/rest/api/sql/databases/createorupdate)를 사용하여 삭제된 데이터베이스를 동일한 SQL Database 서버의 삭제된 데이터베이스에 대한 삭제 시간으로 복원할 수 있습니다. [PowerShell을 사용하여 Managed Instance에서 삭제된 데이터베이스를 복원](https://blogs.msdn.microsoft.com/sqlserverstorageengine/20../../recreate-dropped-database-on-azure-sql-managed-instance)할 수 있습니다. [PowerShell](https://docs.microsoft.com/powershell/module/az.sql/restore-azsqldatabase)을 사용하여 삭제된 데이터베이스를 보존 기간 중 이전 시점으로 복원할 수 있습니다.

> [!TIP]
> 삭제된 데이터베이스를 복원하는 방법을 보여 주는 샘플 PowerShell 스크립트는 [PowerShell을 사용하여 SQL 데이터베이스 복원](scripts/sql-database-restore-database-powershell.md)을 참조하세요.
> [!IMPORTANT]
> Azure SQL Database 서버 인스턴스를 삭제하면 모든 해당 데이터베이스도 삭제되고 복구할 수 없습니다. 현재는 삭제된 서버 복원에 대한 지원이 제공되지 않습니다.

### <a name="deleted-database-restore-using-the-azure-portal"></a>Azure Portal을 사용하여 삭제된 데이터베이스 복원

Azure Portal을 사용하여 [DTU 기반 모델 보존 기간](sql-database-service-tiers-dtu.md) 또는 [vCore 기반 모델 보존 기간](sql-database-service-tiers-vcore.md) 중에 삭제된 데이터베이스를 복구하려면 서버에 대한 페이지를 열고 작업 영역에서 **삭제된 데이터베이스**를 클릭합니다.

![삭제된 데이터베이스 복원-1](./media/sql-database-recovery-using-backups/deleted-database-restore-1.png)

![삭제된 데이터베이스 복원-2](./media/sql-database-recovery-using-backups/deleted-database-restore-2.png)

> [!IMPORTANT]
> 삭제된 데이터베이스를 프로그래밍 방식으로 복원하려면 [자동화된 백업을 사용하여 프로그래밍 방식으로 복구 수행](sql-database-recovery-using-backups.md#programmatically-performing-recovery-using-automated-backups)을 참조하세요.

## <a name="geo-restore"></a>지역 복원

가장 최근의 지역 복제 백업에서 Azure 지역에 있는 서버의 SQL 데이터베이스를 복원할 수 있습니다. 지리적 복원은 지역 중복 백업을 해당 원본으로 사용하고 가동 중단으로 인해 데이터베이스 또는 데이터 센터에 액세스할 수 없는 경우에도 데이터베이스를 복구하는 데 사용될 수 있습니다.

지리적 복원은 데이터베이스가 호스팅되는 지역에 사고가 발생하여 데이터베이스를 사용할 수 없게 되었을 때를 위한 기본 복구 옵션입니다. 지역에서 대규모 인시던트로 인해 데이터베이스 애플리케이션을 사용할 수 없게 되면 지역에서 복제된 백업에서 다른 지역에 있는 서버로 데이터베이스를 복원할 수 있습니다. 백업을 만들 때와 다른 지역에 있는 Azure Blob으로 지역 복제하는 사이에 지연이 있습니다. 재해가 발생한 경우 최대 1시간 동안의 데이터가 손실되므로 이 지연은 최대 1시간일 수 있습니다. 다음 그림에서는 다른 지역에서 마지막으로 사용할 수 있는 백업에서 데이터베이스의 복원을 보여 줍니다.

![geo-restore](./media/sql-database-geo-restore/geo-restore-2.png)

> [!TIP]
> 지역 복원을 수행하는 방법을 보여 주는 샘플 PowerShell 스크립트는 [PowerShell을 사용하여 SQL 데이터베이스 복원](scripts/sql-database-restore-database-powershell.md)을 참조하세요.

지역 보조 복제본에 대한 지정 시간 복원은 현재 지원되지 않습니다. 주 데이터베이스에서만 지정 시간 복원을 수행할 수 있습니다. 지역 복원 기능을 사용하여 가동 중단에서 복구하는 방법에 대한 자세한 내용은 [가동 중단에서 복구](sql-database-disaster-recovery.md)를 참조하세요.

> [!IMPORTANT]
> 백업에서 복원은 RPO(복구 지점 목표)와 ERT(예상 복구 시간)가 가장 긴 SQL Database에서 사용할 수 있는 재해 복구 솔루션 중 가장 기본적인 기능입니다. 작은 크기의 데이터베이스를 사용하는 솔루션의 경우(예: 기본 서비스 계층 또는 탄력적 풀에서 작은 크기의 테넌트 데이터베이스) 최대 ERT가 12시간(대부분 그 이하)인 지역 복제는 적절한 DR 솔루션인 경우가 많습니다. 복구 시간을 줄여야 하는 대규모 데이터베이스를 사용하는 솔루션의 경우 [활성 지역 복제](sql-database-active-geo-replication.md) 또는 [자동 장애 조치(failover) 그룹](sql-database-auto-failover-group.md)을 사용하는 것이 좋습니다. 활성 지역 복제는 지속적으로 복제된 보조 데이터베이스에 대한 장애 조치를 시작하도록 하여 훨씬 더 낮은 RPO와 ERT를 제공합니다. 자동 장애 조치(failover) 그룹을 사용하면 데이터베이스 그룹에 대해 자동 장애 조치(Failover)를 수행할 수 있습니다. 비즈니스 연속성 선택에 대한 자세한 내용은 [비즈니스 연속성 개요](sql-database-business-continuity.md)를 참조하세요.

### <a name="geo-restore-using-the-azure-portal"></a>Azure Portal을 사용한 지역 복원

Azure Portal을 사용하여 [DTU 기반 모델 보존 기간](sql-database-service-tiers-dtu.md) 또는 [vCore 기반 모델 보존 기간](sql-database-service-tiers-vcore.md) 중에 데이터베이스를 지역 복원하려면 SQL Databases 페이지를 연 다음, **추가**를 클릭합니다. **Select source**(소스 선택) 텍스트 상자에서 **Backup**을 선택합니다. 선택한 서버 또는 지역에서 복구를 수행할 백업을 지정합니다.

> [!Note]
> 지역에서 복원은 Azure portal을 사용 하 여 관리 되는 인스턴스에서 사용할 수 없는 경우 PowerShell을 대신 사용 하십시오.

## <a name="programmatically-performing-recovery-using-automated-backups"></a>자동화된 백업을 사용하여 프로그래밍 방식으로 복구 수행

앞서 설명한 것처럼 Azure Portal 외에, Azure PowerShell 또는 REST API를 사용하여 데이터베이스 복구를 프로그래밍 방식으로 수행할 수 있습니다. 다음 표는 사용 가능한 명령의 집합을 보여 줍니다.

### <a name="powershell"></a>PowerShell

[!INCLUDE [updated-for-az](../../includes/updated-for-az.md)]
> [!IMPORTANT]
> Azure SQL Database, Azure Resource Manager PowerShell 모듈은 계속 지원 하지만 Az.Sql 모듈에 대 한 모든 향후 개발 됩니다. 이러한 cmdlet에 대 한 참조 [AzureRM.Sql](https://docs.microsoft.com/powershell/module/AzureRM.Sql/)합니다. Az 모듈에는 AzureRm 모듈의 명령에 대 한 인수를 실질적으로 동일합니다.

- 독립 실행형 또는 풀링된 데이터베이스를 복원 하려면 참조 [복원 AzSqlDatabase](/powershell/module/az.sql/restore-azsqldatabase)합니다.

  | Cmdlet | 설명 |
  | --- | --- |
  | [Get-AzSqlDatabase](/powershell/module/az.sql/get-azsqldatabase) |하나 이상의 데이터베이스를 가져옵니다. |
  | [Get-AzSqlDeletedDatabaseBackup](/powershell/module/az.sql/get-azsqldeleteddatabasebackup) | 복원할 수 있는 삭제된 데이터베이스를 가져옵니다. |
  | [Get-AzSqlDatabaseGeoBackup](/powershell/module/az.sql/get-azsqldatabasegeobackup) |데이터베이스의 지역 중복 백업을 가져옵니다. |
  | [Restore-AzSqlDatabase](/powershell/module/az.sql/restore-azsqldatabase) |SQL 데이터베이스를 복원합니다. |

  > [!TIP]
  > 데이터베이스에 대한 특정 시점 복원을 수행하는 방법을 보여 주는 샘플 PowerShell 스크립트는 [PowerShell을 사용하여 SQL 데이터베이스 복원](scripts/sql-database-restore-database-powershell.md)을 참조하세요.

- 관리 되는 인스턴스로 데이터베이스를 복원 하려면 참조 [복원 AzSqlInstanceDatabase](/powershell/module/az.sql/restore-azsqlinstancedatabase)합니다.

  | Cmdlet | 설명 |
  | --- | --- |
  | [Get-AzSqlInstance](/powershell/module/az.sql/get-azsqlinstance) |하나 이상의 관리 되는 인스턴스를 가져옵니다. |
  | [Get-AzSqlInstanceDatabase](/powershell/module/az.sql/get-azsqlinstancedatabase) | 데이터베이스를 인스턴스를 가져옵니다. |
  | [Restore-AzSqlInstanceDatabase](/powershell/module/az.sql/restore-azsqlinstancedatabase) |인스턴스에 데이터베이스를 복원합니다. |

### <a name="rest-api"></a>REST API

REST API를 사용하여 단일 또는 풀링된 데이터베이스를 복원하려면:

| API | 설명 |
| --- | --- |
| [REST(createMode=Recovery)](https://docs.microsoft.com/rest/api/sql/databases) |데이터베이스를 복원합니다. |
| [데이터베이스 만들기 또는 업데이트 상태 가져오기](https://docs.microsoft.com/rest/api/sql/operations) |복원 작업 동안 상태를 반환합니다. |

### <a name="azure-cli"></a>Azure CLI

- Azure CLI를 사용하여 단일 또는 풀링된 데이터베이스를 복원하려면 [az sql db restore](/cli/azure/sql/db#az-sql-db-restore)를 참조하세요.
- Azure CLI를 사용 하 여 관리 되는 인스턴스를 복원 하려면 참조 [az sql midb에서 복원](/cli/azure/sql/midb#az-sql-midb-restore)

## <a name="summary"></a>요약

자동 백업은 사용자 및 애플리케이션 오류, 우발적인 데이터베이스 삭제 및 장시간의 가동 중단에서 데이터베이스를 보호합니다. 이 기본 제공 기능은 모든 서비스 계층 및 계산 크기에 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계

- 비즈니스 연속성의 개요 및 시나리오를 보려면 [비즈니스 연속성 개요](sql-database-business-continuity.md)를 참조하세요.
- Azure SQL Database 자동화 백업에 대한 자세한 내용은 [SQL Database 자동화 백업](sql-database-automated-backups.md)을 참조하세요.
- 장기 보존에 대해 알아보려면 [장기 보존](sql-database-long-term-retention.md)을 참조하세요.
- 빠른 복구 옵션에 대해 알아보려면 [활성 지역 복제](sql-database-active-geo-replication.md) 또는 [자동 장애 조치(failover) 그룹](sql-database-auto-failover-group.md)을 참조하세요.
