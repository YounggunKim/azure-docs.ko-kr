---
title: Azure Site Recovery 서비스를 사용하여 재해 복구를 위해 보조 Azure 지역에 복제된 Azure IaaS VM에 대한 장애 조치(failover) 및 장애 복구(failback)를 수행합니다.
description: Azure Site Recovery 서비스를 사용하여 재해 복구를 위해 보조 Azure 지역에 복제된 Azure VM에 대한 장애 조치(failover) 및 장애 복구(failback)를 수행하는 방법을 알아봅니다.
services: site-recovery
author: rayne-wiselman
manager: carmonm
ms.service: site-recovery
ms.topic: tutorial
ms.date: 12/27/2018
ms.author: raynew
ms.custom: mvc
ms.openlocfilehash: 46dae28fd6c9eaa3d5e03f5f06c5e92449653679
ms.sourcegitcommit: 90c6b63552f6b7f8efac7f5c375e77526841a678
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2019
ms.locfileid: "56737725"
---
# <a name="fail-over-and-fail-back-azure-vms-between-azure-regions"></a>Azure 지역 간에 Azure VM 장애 조치(Failover) 및 장애 복구

[Azure Site Recovery](site-recovery-overview.md) 서비스는 온-프레미스 컴퓨터와 Azure VM(Virtual Machines)의 복제, 장애 조치(failover), 장애 복구(failback)를 관리 및 오케스트레이션하여 재해 복구 전략에 기여합니다.

이 자습서에서는 단일 Azure VM을 보조 Azure 지역에 장애 조치(failover)하는 방법을 설명합니다. 장애 조치(Failover)한 후에 주 지역이 사용 가능해지면 장애 복구(failback)합니다. 이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Azure VM 장애 조치(failover)
> * 주 지역에 복제되도록 보조 Azure VM 다시 보호
> * 보조 VM 장애 복구(failback)
> * 보조 지역으로 주 VM 다시 보호

> [!NOTE]
> 이 자습서는 대상 영역으로 장애 조치하여 최소 사용자 지정으로 복구하는 단계로 사용자를 안내하기 위한 것입니다. 네트워킹 고려 사항, 자동화 또는 문제 해결을 포함해 장애 조치와 관련된 다양한 측면에 대해 자세히 알아보고 싶다면 Azure VM에 대한 ‘방법’에 있는 문서를 참조하세요.

## <a name="prerequisites"></a>필수 조건

- [재해 복구 드릴](azure-to-azure-tutorial-dr-drill.md)을 완료하여 모든 항목이 예상대로 작동하는지 확인합니다.
- 테스트 장애 조치(failover)를 실행하기 전에 VM 속성을 확인합니다. VM은 [Azure 요구 사항](azure-to-azure-support-matrix.md#replicated-machine-operating-systems)을 준수해야 합니다.

## <a name="run-a-failover-to-the-secondary-region"></a>보조 지역으로 장애 조치(failover) 실행

1. **복제된 항목**에서 장애 조치(failover)할 VM > **장애 조치(Failover)** 를 선택합니다.

   ![장애 조치(failover)](./media/azure-to-azure-tutorial-failover-failback/failover.png)

2. **장애 조치(Failover)** 에서 장애 조치(failover)할 **복구 지점**을 선택합니다. 다음 옵션 중 하나를 사용할 수 있습니다.

   * **최신**(기본값): 이 옵션은 Site Recovery 서비스의 모든 데이터를 처리하고 가장 낮은 RPO(복구 지점 목표)를 제공합니다.
   * **가장 최근에 처리됨**: 이 옵션은 Site Recovery 서비스에서 처리한 최근 복구 지점으로 가상 머신을 되돌립니다.
   * **사용자 지정**: 특정 복구 지점으로 장애 조치(failover)하려면 이 옵션을 사용합니다. 이 옵션은 테스트 장애 조치(failover)를 수행하는 데 유용합니다.

3. 장애 조치를 트리거하기 전에 Site Recovery에서 원본 가상 머신을 종료하려고 시도하는 경우 **장애 조치(failover)를 시작하기 전에 컴퓨터를 종료합니다**를 선택합니다. 종료가 실패하더라도 장애 조치는 계속됩니다. Site Recovery는 장애 조치 후 원본을 정리하지 않습니다.

4. **작업** 페이지에서 장애 조치(failover) 진행 상황을 확인합니다.

5. 장애 조치 후에 가상 컴퓨터에 로그인하여 해당 가상 컴퓨터의 유효성을 검사합니다. 가상 머신에 대한 다른 복구 지점으로 이동하려면 **복구 지점 변경** 옵션을 사용할 수 있습니다.

6. 장애 조치된 가상 머신에 만족하면 장애 조치를 **커밋**할 수 있습니다.
   커밋하면 서비스와 함께 사용할 수 있는 모든 복구 지점이 삭제됩니다. **복구 지점 변경** 옵션은 더 이상 사용할 수 없습니다.

## <a name="reprotect-the-secondary-vm"></a>보조 VM 다시 보호

VM의 장애 조치(failover) 후 주 지역에 다시 복제되도록 다시 보호해야 합니다.

1. VM이 **장애 조치(Failover) 커밋** 상태이고 주 지역을 사용할 수 있는지 확인하면 새 리소스를 만들고 액세스할 수 있습니다.
2. **자격 증명 모음** > **복제된 항목**에서 장애 조치(failover)된 VM을 마우스 오른쪽 단추로 클릭한 다음 **다시 보호**를 선택합니다.

   ![마우스 오른쪽 단추를 클릭하여 다시 보호](./media/azure-to-azure-tutorial-failover-failback/reprotect.png)

2. 보조 지역에서 주 지역으로의 보호 방향이 이미 선택되어 있습니다.
3. **리소스 그룹, 네트워크, 저장소 및 가용성 집합** 정보를 검토합니다. (신규)가 표시된 리소스는 다시 보호 작업의 일부로 생성되었습니다.
4. **확인**을 클릭하여 다시 보호 작업을 트리거합니다. 이 작업은 최신 데이터로 대상 사이트를 시드합니다. 그런 다음 델타를 주 지역에 복제합니다. 이제 VM이 보호된 상태입니다.

> [!NOTE]
> 다시 보호 작업 흐름과 다시 보호 중에 발생하는 작업에 대한 자세한 내용은 [“방법” 섹션](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-how-to-reprotect#what-happens-during-reprotection)을 참조하세요.


## <a name="fail-back-to-the-primary-region"></a>주 지역으로 장애 복구(failback)

VM이 다시 보호된 후 필요에 따라 주 지역으로 장애 복구(failback)할 수 있습니다. 이렇게 하려면 이 문서의 설명에 따라 보조 지역에서 주 지역으로의 장애 조치(failover)를 설정합니다.

![마우스 오른쪽 단추를 클릭하여 다시 보호](./media/azure-to-azure-tutorial-failover-failback/failback.png)

위의 스크린샷을 보면 “ContosoWin2016” VM이 미국 중부에서 미국 동부로 장애 조치(failover)되었다가 미국 동부에서 미국 중부로 장애 복구(failback)되었습니다.

장애 조치(failover)로 인해 보조 지역 즉, 재해 복구 지역의 VM은 종료되고, 주 지역에서 VM이 생성되어 부팅됩니다. 위에 나온 것처럼 DR VM이 정지 할당 취소 상태로 유지됨을 **참고**하세요. 이 동작은 Azure Site Recovery가 가상 머신의 정보를 저장하므로 계획적인 것입니다. 이는 나중에 주 지역을 보조 지역으로 장애 조치(failover)하는 데 유용할 수 있습니다. 할당 취소된 가상 머신에 대해서는 요금이 부과되지 않으므로 그대로 유지해야 합니다.
