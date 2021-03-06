---
title: Azure 리소스에 대한 RBAC 문제 해결 | Microsoft Docs
description: Azure 리소스에 대한 RBAC(역할 기반 액세스 제어) 문제를 해결합니다.
services: azure-portal
documentationcenter: na
author: rolyon
manager: mtillman
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: role-based-access-control
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 03/24/2019
ms.author: rolyon
ms.reviewer: bagovind
ms.custom: seohack1
ms.openlocfilehash: d85c49cc8533b88382de81f8f12fde7116afb69a
ms.sourcegitcommit: 280d9348b53b16e068cf8615a15b958fccad366a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/25/2019
ms.locfileid: "58407592"
---
# <a name="troubleshoot-rbac-for-azure-resources"></a>Azure 리소스에 대한 RBAC 문제 해결

이 문서에서는 Azure 리소스에 대한 RBAC(역할 기반 액세스 제어)와 관련된 일반적인 질문에 대답합니다. Azure Portal의 역할을 사용할 때 예상되는 동작을 이해하고 액세스 문제를 해결하는 데 도움이 될 것입니다.

## <a name="problems-with-rbac-role-assignments"></a>RBAC 역할 할당 관련 문제

- Azure portal에서 역할 할당에 추가할 수 없는 경우 **액세스 제어 (IAM)** 때문에 **추가** > **역할 할당 추가** 옵션은 사용할 수 없습니다. 또는 오류가 발생 하면 권한을 "개체 id 사용 하 여 클라이언트 없는 작업을 수행 하려면 권한 부여", 때문에 있는 역할이 할당 된 사용자로 로그인 현재 등록 되어 있는지 확인 합니다 `Microsoft.Authorization/roleAssignments/write` 와 같은 권한을 [소유자](built-in-roles.md#owner) 나 [사용자 액세스 관리자](built-in-roles.md#user-access-administrator) 역할을 할당 하려는 범위에 있습니다.
- 오류 메시지를 받게 되 면 "없습니다 더 이상의 역할 할당을 만들 수 있습니다 (코드: RoleAssignmentLimitExceeded) "역할을 할당 하려고 할 때 그룹 대신 역할을 할당 하 여 역할 할당의 수를 줄이기 위해 시도 합니다. Azure는 구독당 최대 **2000**개의 역할 할당을 지원합니다.

## <a name="problems-with-custom-roles"></a>사용자 지정 역할의 문제

- 사용자 지정 역할을 만드는 방법에 대 한 단계에 필요한 경우에 사용 하 여 사용자 지정 역할 자습서를 참조 하세요 [Azure PowerShell](tutorial-custom-role-powershell.md) 하거나 [Azure CLI](tutorial-custom-role-cli.md)합니다.
- 기존 사용자 지정 역할을 업데이트할 수 없는 경우에 역할이 할당 된 사용자로 로그인 현재 등록 되어 있는지 확인 합니다 `Microsoft.Authorization/roleDefinition/write` 와 같은 권한이 [소유자](built-in-roles.md#owner) 또는 [사용자 액세스 관리자](built-in-roles.md#user-access-administrator).
- 사용자 지정 역할을 삭제 하는 오류 메시지를 가져올 수 없는 경우 "기존 역할을 참조 하는 역할 할당 (코드: RoleDefinitionHasAssignments) ", 여전히 사용자 지정 역할을 사용 하 여 역할 할당은 있습니다. 이러한 역할 할당을 제거 하 고 사용자 지정 역할을 다시 삭제 해 보십시오.
- "역할 정의 제한을 초과 했습니다 오류 메시지를 받게 되 면. 더 이상 없는 역할 정의 만들 수 있습니다 (코드: RoleDefinitionLimitExceeded) "새 사용자 지정 역할을 만들 하려고 할 때 사용 되지 않는 모든 사용자 지정 역할을 삭제 합니다. Azure는 테넌트에서 최대 **2000**개의 사용자 지정 역할을 지원합니다.
- 하지만 오류가 발생에 있는 것 처럼 "클라이언트 연결 된 구독을 찾을 수 없습니다 범위 / {subscriptionid}', 'Microsoft.Authorization/roleDefinitions/write' 작업을 수행할 수 있는 권한이" 하는 경우 사용자 지정 역할을 업데이트 하려고 할 때 확인 여부를 하나 이상의 [할당 가능한 범위](role-definitions.md#assignablescopes) 테 넌 트에서 삭제 되었습니다. 범위 삭제 된 경우 만든 지원 티켓을 지금은 사용할 수 있는 셀프 서비스 솔루션이 없기 때문입니다.

## <a name="recover-rbac-when-subscriptions-are-moved-across-tenants"></a>테넌트에서 구독이 이동될 때 RBAC 복구

- 구독을 전송 하는 방법에 대 한 단계를 보려면 다른 Azure ad 테 넌 트를 참조 하세요 [다른 계정으로 Azure 구독의 소유권 이전](../billing/billing-subscription-transfer.md)합니다.
- 구독을 전송 하는 경우를 다른 Azure AD 테 넌 트, 모든 역할 할당 원본 Azure AD 테 넌 트에서 영구적으로 삭제 되 고 대상 Azure AD 테 넌 트에 마이그레이션되지 않습니다. 대상 테넌트에서 역할 할당을 다시 만들어야 합니다.
- Azure AD를 있다면 있습니다 및 전역 관리자에 액세스할 수 없는 구독 테 넌 트 간에 이동 된 후, 사용 합니다 **Azure 리소스에 대 한 관리 액세스** 를 일시적으로 설정/해제 [액세스권한상승](elevate-access-global-admin.md) 구독에 대 한 액세스를 가져오려고 합니다.

## <a name="issues-with-service-admins-or-co-admins"></a>서비스 관리자 또는 공동 관리자 관련 문제

- 서비스 관리자 또는 공동 관리자를 사용 하 여 문제가 있는, 참조 [Azure 구독 관리자를 추가 또는 변경](../billing/billing-add-change-azure-subscription-administrator.md) 고 [클래식 구독 관리자 역할, Azure RBAC 역할 및 Azure AD 관리자 역할](rbac-and-directory-admin-roles.md)입니다.

## <a name="access-denied-or-permission-errors"></a>액세스 거부 또는 권한 오류

- 사용 권한 오류가 발생할 경우 "개체 id 사용 하 여 클라이언트에 권한 부여 범위에 대해 작업을 수행할 수 없는 (코드: AuthorizationFailed) "리소스를 만들려고 하는 경우 선택한 범위에서 리소스에 쓰기 권한이 있는 역할이 할당 된 사용자로 로그인 현재 등록 되어 있는지 확인 합니다. 예를 들어, 리소스 그룹에 가상 컴퓨터를 관리 하려면 있어야 합니다 [Virtual Machine 참여자](built-in-roles.md#virtual-machine-contributor) 역할 리소스 그룹 (또는 부모 범위). 각 기본 제공 역할에 대 한 사용 권한 목록에 대해서 [Azure 리소스에 대 한 기본 제공 역할](built-in-roles.md)입니다.
- 사용 권한 오류가 발생 하면 "권한이 지원 요청을 만들려면" 만들기 또는 지원 티켓을 업데이트 하려고 할 때에 역할이 할당 된 사용자로 로그인 현재 등록 되어 있는지 확인 합니다 `Microsoft.Support/supportTickets/write` 와같이권한이[지원 요청 기여자](built-in-roles.md#support-request-contributor)합니다.

## <a name="rbac-changes-are-not-being-detected"></a>RBAC 변경 내용이 인식되지 않음

Azure Resource Manager는 경우에 따라 성능 향상을 위해 구성 및 데이터를 캐시합니다. 역할 할당을 만들거나 삭제하는 경우 변경 내용이 적용되는 데 최대 30분이 걸릴 수 있습니다. Azure Portal, Azure PowerShell 또는 Azure CLI를 사용하는 경우 로그아웃 및 로그인하여 역할 할당 변경 내용을 강제로 새로 고칠 수 있습니다. REST API 호출을 사용하여 역할 할당을 변경하는 경우 액세스 토큰을 새로 고쳐 강제로 새로 고칠 수 있습니다.

## <a name="web-app-features-that-require-write-access"></a>쓰기 액세스 권한이 필요한 웹앱 기능

사용자에게 단일 웹앱에 대한 읽기 전용 액세스를 부여하면 예상치 않게 일부 기능을 사용하지 못할 수 있습니다. 다음 관리 기능을 사용하려면 참여자나 소유자에게 제공되는 웹앱에 대한 **쓰기** 권한이 필요하며, 읽기 전용 시나리오에서는 이러한 기능을 사용할 수 없습니다.

* 시작, 중지 등의 명령
* 일반 구성, 규모 설정, 백업 설정, 모니터링 설정 등의 설정 변경
* 게시 자격 증명과 앱 설정, 연결 문자열 등의 기타 암호 액세스
* 스트리밍 로그
* 진단 로그 구성
* 콘솔(명령 프롬프트)
* 활성 및 최근 배포(로컬 Git 연속 배포의 경우)
* 예상 소요 시간
* 웹 테스트
* 가상 네트워크(쓰기 권한이 있는 사용자가 이전에 가상 네트워크를 구성한 경우에만 읽기 권한자에게 표시됨)

이러한 타일에 액세스할 수 없는 경우 관리자에게 웹앱에 대한 참가자 권한을 요청해야 합니다.

## <a name="web-app-resources-that-require-write-access"></a>쓰기 액세스 권한이 필요한 웹앱 리소스

웹앱에서 몇 가지 리소스가 상호 연동되는 경우 웹앱의 구조가 복잡해집니다. 아래에는 웹 사이트 몇 개가 포함된 일반적인 리소스 그룹이 나와 있습니다.

![웹앱 리소스 그룹](./media/troubleshooting/website-resource-model.png)

따라서 사용자에게 웹앱에 대한 권한만 부여하면 Azure Portal에서 웹 사이트 블레이드의 기능을 대부분 사용할 수 없게 됩니다.

다음 항목을 사용하려면 웹 사이트에 해당하는 **App Service 계획**에 대한 **쓰기** 권한이 필요합니다.  

* 웹앱의 가격 책정 계층 보기(무료 또는 표준)  
* 크기 조정 구성(인스턴스 수, 가상 머신 크기, 자동 크기 조정 설정)  
* 할당량(저장소, 대역폭, CPU)  

다음 항목을 사용하려면 웹 사이트를 포함하는 전체 **리소스 그룹**에 대한 **쓰기** 권한이 필요합니다.  

* SSL 인증서 및 바인딩(SSL 인증서는 같은 리소스 그룹과 지리적 위치의 사이트 간에 공유될 수 있음)  
* 경고 규칙  
* 자동 크기 조정 설정  
* Application Insights 구성 요소  
* 웹 테스트  

## <a name="virtual-machine-features-that-require-write-access"></a>쓰기 액세스 권한이 필요한 가상 머신 기능

웹앱과 마찬가지로 가상 머신 블레이드의 일부 기능 역시 가상 머신 또는 리소스 그룹의 기타 리소스에 대한 쓰기 권한이 있어야 사용할 수 있습니다.

가상 머신은 도메인 이름, 가상 네트워크, 저장소 계정 및 경고 규칙과 관련이 있습니다.

다음 항목을 사용하려면 **가상 머신**에 대한 **쓰기** 권한이 필요합니다.

* 엔드포인트  
* IP 주소  
* 디스크  
* 확장  

다음 항목을 사용하려면 **가상 머신**와 가상 머신이 속한 **리소스 그룹**(도메인 이름 포함) 둘 다에 대한 **쓰기** 권한이 필요합니다.  

* 가용성 집합  
* 부하 분산된 집합  
* 경고 규칙  

이러한 타일에 액세스할 수 없는 경우 관리자에게 리소스 그룹에 대한 참가자 권한을 요청합니다.

## <a name="azure-functions-and-write-access"></a>Azure Functions 및 쓰기 액세스

[Azure Functions](../azure-functions/functions-overview.md)의 일부 기능에는 쓰기 액세스 권한이 있어야 합니다. 예를 들어 사용자가 읽기 역할에 할당된 경우 함수 앱 내에서 함수를 볼 수 없습니다. 포털에서는 **(액세스 권한 없음)** 을 표시합니다.

![함수 앱 액세스 권한 없음](./media/troubleshooting/functionapps-noaccess.png)

판독기는 **플랫폼 기능** 탭을 클릭한 다음, **모든 설정**을 클릭하여 함수 앱(웹앱과 유사)에 관련된 일부 설정을 볼 수 있지만 이러한 설정을 수정할 수 없습니다.

## <a name="next-steps"></a>다음 단계
* [RBAC 및 Azure Portal을 사용하여 Azure 리소스에 대한 액세스 관리](role-assignments-portal.md)
* [Azure 리소스에 대한 RBAC 변경 내용의 활동 로그 보기](change-history-report.md)

