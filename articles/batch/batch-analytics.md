---
title: Azure Batch 분석 | Microsoft Docs
description: Azure Batch 분석에 대한 참조입니다.
services: batch
author: laurenhughes
manager: jeconnoc
ms.assetid: ''
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: lahugh
ms.openlocfilehash: 999c3037196044250b8a12d6b6b380553e58c6ba
ms.sourcegitcommit: 698a3d3c7e0cc48f784a7e8f081928888712f34b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2019
ms.locfileid: "55460185"
---
# <a name="batch-analytics"></a>Batch 분석
Batch 분석의 항목에는 Batch 서비스 리소스에 사용할 수 있는 이벤트 및 경고에 대한 참조 정보가 포함되어 있습니다.

Batch 진단 로그를 활성화하고 사용하는 방법에 대한 자세한 내용은 [Azure Batch 진단 로깅](https://azure.microsoft.com/documentation/articles/batch-diagnostics/)을 참조하세요.

## <a name="diagnostic-logs"></a>진단 로그

Azure Batch 서비스는 특정 Batch 리소스의 수명 동안 다음과 같은 진단 로그 이벤트를 내보냅니다.

**서비스 로그 이벤트**
* [풀 만들기](batch-pool-create-event.md)
* [풀 삭제 시작](batch-pool-delete-start-event.md)
* [풀 삭제 완료](batch-pool-delete-complete-event.md)
* [풀 크기 조정 시작](batch-pool-resize-start-event.md)
* [풀 크기 조정 완료](batch-pool-resize-complete-event.md)
* [작업 시작](batch-task-start-event.md)
* [작업 완료](batch-task-complete-event.md)
* [작업 실패](batch-task-fail-event.md)