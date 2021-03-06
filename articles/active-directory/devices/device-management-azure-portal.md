---
title: Azure Portal을 사용하여 디바이스를 관리하는 방법 | Microsoft Docs
description: Azure Portal을 사용하여 디바이스를 관리하는 방법을 알아봅니다.
services: active-directory
documentationcenter: ''
author: MicrosoftGuyJFlo
manager: daveba
editor: ''
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.subservice: devices
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2018
ms.author: joflore
ms.reviewer: jairoc
ms.collection: M365-identity-device-management
ms.openlocfilehash: 516a2d3b0f81bcef1ed636be9d1da9a270cc7069
ms.sourcegitcommit: 6da4959d3a1ffcd8a781b709578668471ec6bf1b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58520023"
---
# <a name="how-to-manage-devices-using-the-azure-portal"></a>Azure Portal을 사용하여 디바이스를 관리하는 방법


Azure AD(Active Directory)의 디바이스 관리를 사용하면 보안 및 규정 준수에 대한 표준을 충족하는 디바이스에서 사용자 리소스에 액세스할 수 있습니다. 

이 문서의 내용:

- 사용자가 [Azure Active Directory의 디바이스 관리 소개](overview.md)를 잘 숙지한 것으로 가정합니다.

- Azure Portal을 사용하여 디바이스 관리에 대한 정보를 제공합니다.

## <a name="manage-devices"></a>디바이스 관리 

Azure Portal에서는 디바이스를 관리하는 중앙 위치를 제공합니다. [직접 링크](https://portal.azure.com/#blade/Microsoft_AAD_IAM/DevicesMenuBlade/Devices)를 사용하거나 다음 수동 단계를 수행하여 이 위치로 이동할 수 있습니다.

1. 관리자 권한으로 [Azure Portal](https://portal.azure.com)에 로그인합니다.

2. 왼쪽 탐색 모음에서 **Active Directory**를 클릭합니다.

    ![디바이스 설정 구성](./media/device-management-azure-portal/01.png)

3. **관리** 섹션에서 **디바이스**를 클릭합니다.

    ![디바이스 설정 구성](./media/device-management-azure-portal/74.png)
 
**디바이스** 페이지에서 다음을 수행할 수 있습니다.

- 디바이스 관리 설정 구성

- 디바이스 찾기

- 디바이스 관리 작업 수행

- 디바이스 관리 관련 감사 로그 검토  
  

## <a name="configure-device-settings"></a>디바이스 설정 구성

Azure Portal을 사용하여 디바이스를 관리하려면 해당 디바이스가 Azure AD에 [등록되거나 조인](overview.md#getting-devices-under-the-control-of-azure-ad)되어야 합니다. 관리자는 디바이스 설정을 구성하여 디바이스 등록 및 조인 프로세스를 구체적으로 조정할 수 있습니다. 

![디바이스 설정 구성](./media/device-management-azure-portal/22.png)

디바이스 설정 페이지에서 다음을 구성할 수 있습니다.

![Intune 디바이스 관리](./media/device-management-azure-portal/21.png)


- **사용자가 Azure AD에 디바이스를 조인할 수 있습니다.** - 이 설정을 사용하여 Azure AD에 [디바이스를 조인](overview.md#azure-ad-joined-devices)할 수 있는 사용자를 선택할 수 있습니다. 기본값은 **모두**입니다. 이 설정은 Windows 10의 Azure AD 조인에만 적용됩니다.

- **Azure AD 조인 디바이스의 추가 로컬 관리자** - 디바이스에서 로컬 관리자 권한이 부여된 사용자를 선택할 수 있습니다. 여기에 추가한 사용자는 Azure AD의 *디바이스 관리자* 역할에 추가됩니다. Azure AD의 전역 관리자 및 디바이스 소유자에게는 기본적으로 로컬 관리자 권한이 부여됩니다. 이 옵션은 Azure AD Premium 또는 EMS(Enterprise Mobility Suite) 등의 제품을 통해 사용할 수 있는 프리미엄 버전 기능입니다. 

- **사용자가 디바이스를 Azure AD에 등록할 수 있습니다.** - 디바이스를 Azure AD에 [등록](overview.md#azure-ad-registered-devices)할 수 있게 하려면 이 설정을 구성해야 합니다. **없음**을 선택하는 경우 디바이스가 Azure AD 조인 또는 하이브리드 Azure AD 조인 디바이스가 아닌 경우 등록할 수 없습니다. Office 365용 Microsoft Intune 또는 MDM(모바일 디바이스 관리)에 등록하려면 먼저 디바이스를 등록해야 합니다. 이러한 서비스 중 하나를 구성한 경우 **모두**가 선택되고 **없음**은 사용할 수 없습니다.

- **디바이스에 연결하려면 Multi-factor Auth 필요** - 사용자가 Azure AD에 디바이스를 [조인](overview.md#azure-ad-joined-devices)하기 위해 또 다른 인증 수단을 제공해야 하는지 여부를 선택할 수 있습니다. 기본값은 **아니요**입니다. 그러나 디바이스를 등록하는 경우 Multi-Factor Authentication을 사용하는 것이 좋습니다. 이 서비스에 대해 Multi-Factor Authentication을 사용하도록 설정하기 전에 디바이스를 등록하는 사용자에 대해 Multi-Factor Authentication을 구성해야 합니다. 다양한 Azure Multi-Factor Authentication 서비스에 대한 자세한 내용은 [Azure Multi-Factor Authentication 시작](../authentication/concept-mfa-whichversion.md)을 참조하세요. 이 설정은 Windows 10 또는 Windows 7에 대한 하이브리드 조인에는 영향을 주지 않습니다. Windows 10의 Azure AD 조인 및 Windows 10/iOS/Android의 BYO 디바이스 등록에만 이 설정이 적용됩니다. 

- **최대 디바이스 수** - 이 설정을 사용하여 Azure AD에서 사용자가 보유할 수 있는 디바이스의 최대 수를 선택할 수 있습니다. 사용자가 이 할당량에 도달하는 경우 기존 디바이스 중 하나 이상이 제거될 때까지 디바이스를 더 추가할 수 없습니다. 디바이스 견적은 현재 Azure AD에 조인되었거나 Azure AD에 등록된 모든 디바이스에 대해 계산됩니다. 기본값은 **20**입니다.

- **사용자자 디바이스 간에 설정 및 앱 데이터를 동기화할 수 있음** - 기본적으로 이 설정은 **없음**으로 지정됩니다. 특정 사용자 또는 그룹을 선택하거나 모두를 선택하면 Windows 10 디바이스 간에 사용자 설정 및 앱 데이터를 동기화할 수 있습니다. Windows 10에서 동기화가 작동되는 방식에 대해 자세히 알아봅니다.
이 옵션은 Azure AD Premium 또는 EMS(Enterprise Mobility Suite) 등의 제품을 통해 사용할 수 있는 프리미엄 기능입니다.





## <a name="locate-devices"></a>디바이스 찾기

두 가지 옵션으로 등록 및 조인된 디바이스를 찾을 수 있습니다.

- **디바이스** 페이지의 **관리** 섹션에 있는 **모든 디바이스**  

    ![모든 디바이스](./media/device-management-azure-portal/41.png)


- **사용자** 페이지의 **관리** 섹션에 있는 **디바이스**
 
    ![모든 디바이스](./media/device-management-azure-portal/43.png)



두 옵션 모두에서 다음과 같은 보기가 표시될 수입니다.


- 표시 이름을 사용하는 디바이스를 필터로 검색할 수 있습니다.

- 등록 및 조인된 디바이스의 자세한 개요를 제공합니다.

- 일반 디바이스 관리 작업을 수행할 수 있습니다.
   

![모든 디바이스](./media/device-management-azure-portal/51.png)

일부 iOS 디바이스의 경우 아포스트로피를 포함하는 디바이스 이름이 아포스트로피처럼 보이는 다른 문자를 사용할 수 있습니다. 이러한 디바이스를 검색하는 것은 약간 까다로울 수 있습니다. 따라서 검색 결과가 올바르게 표시되지 않으면 검색 문자열에 일치하는 아포스트로피 문자가 포함되어 있는지 확인하세요.

## <a name="device-management-tasks"></a>디바이스 관리 작업

전역 관리자 또는 클라우드 장치 관리자를 등록 또는 조인 된 장치를 관리할 수 있습니다. Intune 서비스 관리자는 다음을 수행할 수 있습니다.
 
- 디바이스 업데이트 - 예제는 디바이스를 사용/사용 안 함과 같은 일상적인 작업임

- 디바이스 삭제 - 디바이스가 사용 중지되고 Azure AD에서 삭제돼야 하는 경우

이 섹션에서는 일반 디바이스 관리 작업에 대한 정보를 제공합니다.



### <a name="manage-an-intune-device"></a>Intune 디바이스 관리

Intune 관리자인 경우 **Microsoft Intune**으로 표시된 디바이스를 관리할 수 있습니다. 

![Intune 디바이스 관리](./media/device-management-azure-portal/31.png)


### <a name="enable--disable-an-azure-ad-device"></a>Azure AD 디바이스 사용/사용 안 함

디바이스를 사용/사용 안 함으로 설정하려면 두 가지 옵션이 있습니다.

- **모든 디바이스** 페이지의 작업 메뉴("…")

    ![Intune 디바이스 관리](./media/device-management-azure-portal/71.png)

- **디바이스** 페이지의 도구 모음

    ![Intune 디바이스 관리](./media/device-management-azure-portal/32.png)


**설명**

- 전역 관리자 여야 하거나 장치 관리자는 장치 사용 안 함 / 사용 하려면 Azure AD에서 클라우드를 해야 합니다. 
- 장치를 사용 하지 않도록 설정 하므로 장치 CA에 의해 보호 되는 Azure AD 리소스에 액세스 하거나 WH4B 자격 증명을 사용 하 여 장치를 방지 하는 Azure AD를 사용 하 여 성공적으로 인증에서 장치 수 없게 합니다. 



### <a name="delete-an-azure-ad-device"></a>Azure AD 디바이스 삭제

디바이스를 삭제하려면 두 가지 옵션이 있습니다.

- **모든 디바이스** 페이지의 작업 메뉴("…")

    ![Intune 디바이스 관리](./media/device-management-azure-portal/72.png)

- **디바이스** 페이지의 도구 모음

    ![디바이스 삭제](./media/device-management-azure-portal/34.png)


**설명**

- 장치를 삭제하려면 Azure AD에서 글로벌 관리자 또는 Intune 관리자여야 합니다.

- 디바이스 삭제:
 
    - 디바이스에서 Azure AD 리소스에 액세스할 수 없게 됩니다. 

    - 디바이스에 연결되어 있는 모든 세부 정보(예: Windows 디바이스에 대한 BitLocker 키)를 제거합니다.  

    - 복구할 수 없으며, 반드시 필요한 경우가 아니면 권장되지 않는 작업을 나타냅니다.

디바이스를 다른 관리 기관(예: Microsoft Intune)에서 관리하는 경우 Azure AD에서 디바이스를 삭제하기 전에 디바이스를 초기화/사용 중지했는지 확인합니다.

 


### <a name="view-or-copy-device-id"></a>디바이스 ID 확인 또는 복사

디바이스 ID를 사용하여 디바이스의 디바이스 ID 세부 정보를 확인하거나 문제 해결 동안 PowerShell을 사용할 수 있습니다. 복사 옵션에 액세스하려면 디바이스를 클릭합니다.

![디바이스 ID 보기](./media/device-management-azure-portal/35.png)
  

### <a name="view-or-copy-bitlocker-keys"></a>BitLocker 키 확인 또는 복사

BitLocker 키를 보고 복사하여 사용자가 암호화된 드라이브를 복구하도록 지원할 수 있습니다. 이러한 키는 암호화되고 해당 키가 Azure AD에 저장된 Windows 디바이스에 대해서만 사용할 수 있습니다. 디바이스 세부 정보에 액세스할 때 이러한 키를 복사할 수 있습니다.
 
![BitLocker 키 보기](./media/device-management-azure-portal/36.png)

BitLocker 키를 보거나 복사하려면, 디바이스의 소유자 또는 다음 역할 중 하나 이상이 할당된 사용자여야 합니다.

- 전역 관리자
- 기술 지원팀 관리자
- 보안 관리자
- 보안 읽기 권한자
- Intune 서비스 관리자

> [!NOTE]
> 하이브리드 Azure AD 조인 Windows 10 디바이스에는 소유자가 없습니다. 따라서 소유자로 디바이스를 찾으려는 경우 찾지 못하면 디바이스 ID로 검색합니다.


## <a name="audit-logs"></a>감사 로그


디바이스 활동은 활동 로그를 통해 사용할 수 있습니다. 여기에는 디바이스 등록 서비스 및 사용자가 트리거한 작업이 포함됩니다.

- 디바이스 만들기 및 디바이스에 소유자/사용자 추가

- 디바이스 설정 변경

- 디바이스 삭제 또는 업데이트 등의 디바이스 작업
 
감사 데이터에 대한 진입점은 **디바이스** 페이지의 **작업** 섹션에 있는 **감사 로그**입니다.

![감사 로그](./media/device-management-azure-portal/61.png)


감사 로그에는 다음 항목을 보여 주는 기본 목록 보기가 있습니다.

- 발생 날짜와 시간

- 대상

- 작업의 초기자/행위자(누가)

- 작업(무엇)

![감사 로그](./media/device-management-azure-portal/63.png)

도구 모음에서 **열**을 클릭하여 목록 보기를 사용자 지정할 수 있습니다.
 
![감사 로그](./media/device-management-azure-portal/64.png)


보고된 데이터를 자신에게 적합한 수준으로 좁히려면 다음 필드를 사용하여 감사 데이터를 필터링할 수 있습니다.

- Category
- 활동 리소스 종류
- 작업
- 날짜 범위
- 대상
- 초기자(작업자)

필터 이외의 방법으로도 특정 항목을 검색할 수 있습니다.

![감사 로그](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a>다음 단계

* [Azure Active Directory의 디바이스 관리 소개](overview.md)



