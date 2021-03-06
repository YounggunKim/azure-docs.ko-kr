---
title: Microsoft Authenticator 앱을 사용하여 계정에 로그인 - Azure Active Directory | Microsoft Docs
description: Microsoft Authenticator 앱을 사용하여 2단계 인증 또는 휴대폰 로그인을 통해 회사 또는 학교 계정 또는 개인 Microsoft 및 Microsoft 이외의 계정에 로그인합니다.
services: active-directory
author: eross-msft
manager: daveba
ms.service: active-directory
ms.workload: identity
ms.subservice: user-help
ms.topic: conceptual
ms.date: 01/24/2019
ms.author: lizross
ms.reviewer: olhaun
ms.collection: M365-identity-device-management
ms.openlocfilehash: bc136cdc88c67e3b26aefc4982f49a2547e456db
ms.sourcegitcommit: 49c8204824c4f7b067cd35dbd0d44352f7e1f95e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58370094"
---
# <a name="sign-in-to-your-accounts-using-the-microsoft-authenticator-app"></a>Microsoft Authenticator 앱을 사용하여 계정에 로그인
2단계 인증을 사용하는 경우 Microsoft Authenticator 앱으로 계정에 쉽게 로그인할 수 있습니다. 2단계 인증을 사용하면 특히 중요한 정보를 볼 때 보다 안전하게 계정에 액세스할 수 있습니다. 암호를 잊어버리거나 암호가 노출될 수 있으므로 2단계 인증은 다른 사람이 침입하기 어렵게 만들어서 계정을 보호하는 추가 보안 단계입니다.

Microsoft Authenticator 앱은 다음을 비롯한 여러 가지 방법으로 사용할 수 있습니다.

- 사용자 이름 및 암호로 로그인한 후 두 번째 확인 방법에 대한 프롬프트를 제공합니다.

- 암호를 요구하지 않고 모바일 디바이스에서 사용자 이름과 지문, 얼굴 또는 PIN을 사용하여 로그인합니다.

  >[!Important]
  >이 휴대폰 로그인 방법은 회사 또는 학교 및 개인 Microsoft 계정에서만 작동합니다. Microsoft 이외의 계정은 표준 2단계 인증 프로세스를 사용해야 합니다.

## <a name="prerequisites"></a>필수 조건
Microsoft Authenticator 앱을 사용하려면 다음을 수행해야 합니다.

 1. Microsoft Authenticator 앱을 다운로드하고 설치합니다. 이를 아직 수행하지 않은 경우 [앱 다운로드 및 설치](user-help-auth-app-download-install.md)를 참조하세요.

 2. Microsoft Authenticator 앱에 회사/학교, 개인 및 타사 계정을 추가합니다. 자세한 단계는 [회사 또는 학교 계정 추가](user-help-auth-app-add-work-school-account.md), [개인 계정 추가](user-help-auth-app-add-personal-ms-account.md) 및 [Microsoft 이외의 계정 추가](user-help-auth-app-add-non-ms-account.md)를 참조하세요.

## <a name="turn-on-and-use-phone-sign-in-for-your-work-or-school-account"></a>회사 또는 학교 계정에 휴대폰 로그인 설정 및 사용
휴대폰 로그인은 2단계 인증의 형식입니다. 알고 있고 가지고 있는 것을 제공하여 여전히 ID를 확인해야 하지만 휴대폰 로그인을 통해 계정 암호 입력을 건너뛸 수 있으며 모바일 디바이스에서 모든 ID 검증을 수행합니다.

휴대폰 로그인을 설정하려면 2단계 인증을 설정해야 합니다. 계정에 대한 2단계 인증을 설정하는 방법에 대한 자세한 내용은 [회사 또는 학교 계정 추가](user-help-auth-app-add-work-school-account.md) 및 [개인 계정 추가](user-help-auth-app-add-personal-ms-account.md)를 참조하세요.

휴대폰 로그인은 iOS 디바이스 및 Android 6.0 이상을 실행하는 Android 디바이스에서만 사용할 수 있습니다.

### <a name="turn-on-phone-sign-in"></a>휴대폰 로그인 설정 

- Microsoft Authenticator 앱을 열고, 회사 또는 학교 계정으로 이동하고, 휴대폰 로그인을 설정합니다.

    - **이 아이콘 ![설정을 보여주는 아이콘](media/user-help-auth-app-sign-in/icon.png)이 있는 경우** 이 아이콘이 회사 또는 학교 계정 이름 옆에 나타나는 경우 계정에 대한 휴대폰 로그인을 이미 설정했음을 의미합니다. 앱 외부에서 인증 요청에 대한 알림을 받을 수 있도록 계정에 대한 푸시 알림을 추가하라는 메시지가 표시될 수 있습니다.

    - **2단계 인증에 대한 앱을 사용하고 있는 경우** 앱 및 2단계 인증을 이미 사용하고 있는 경우 계정 이름 옆의 드롭다운 화살표를 선택한 다음, **휴대폰 로그인 사용**을 선택할 수 있습니다.
    
    - **회사 또는 학교 계정을 찾을 수 없는 경우** 앱의 **계정** 화면에서 회사 또는 학교 계정을 찾을 수 없는 경우 앱에 계정을 아직 추가하지 않은 것을 의미합니다. [회사 또는 학교 계정 추가](user-help-auth-app-add-work-school-account.md) 문서의 단계를 수행하여 회사 또는 학교 계정을 추가합니다.

### <a name="sign-in-to-your-account-using-phone-sign-in"></a>휴대폰 로그인을 사용하여 계정에 로그인
휴대폰 로그인을 설정한 후 Microsoft Authenticator 앱만을 사용하여 로그인할 수 있습니다.

1. 회사 또는 학교 계정에 로그인합니다.

    사용자 이름을 입력하면 2자리 숫자를 보여주고 Microsoft Authenticator 앱을 통해 로그인하라는 **로그인 승인** 화면이 나타납니다. 이 로그인 방법을 사용하지 않으려면 **암호를 대신 사용**하도록 선택하고, 암호를 사용하여 로그인합니다.

    ![컴퓨터의 로그인 승인 상자](media/user-help-auth-app-sign-in/microsoft-auth-app-sign-in.png)

2. 디바이스에서 알림 또는 Microsoft Authenticator 앱을 연 다음, 컴퓨터의 **로그인 승인** 화면에 표시되는 숫자와 일치하는 숫자를 탭합니다.

    ![디바이스의 로그인 승인 상자](media/user-help-auth-app-sign-in/microsoft-auth-app-sign-in-numbers.png)

3. 로그인 시도를 인식한 경우 **승인**을 선택합니다. 그렇지 않은 경우 **거부**를 선택합니다.

4. 휴대폰의 PIN 또는 생체 인식 키를 사용하여 인증을 완료합니다.

## <a name="turn-on-and-use-phone-sign-in-for-your-personal-microsoft-accounts"></a>개인 Microsoft 계정에 휴대폰 로그인 설정 및 사용
Outlook.com, Xbox, Skype 등의 개인 Microsoft 계정에 휴대폰 로그인할 사용할 수 있습니다.

>[!NOTE]
>계정을 보호하기 위해 Microsoft Authenticator 앱에서 디바이스의 PIN 또는 생체 인식을 잠글 것을 요구합니다. 휴대폰을 잠금 해제 상태로 유지하면 휴대폰 로그인을 활성화하기 전에 보안 잠금을 설정하라고 앱에서 요구합니다.

### <a name="turn-on-phone-sign-in"></a>휴대폰 로그인 설정 

- Microsoft Authenticator 앱을 열고, 개인 Microsoft 계정으로 이동하고, 휴대폰 로그인을 설정합니다.

    - **이 아이콘 ![설정을 보여주는 아이콘](media/user-help-auth-app-sign-in/icon.png)이 있는 경우** 이 아이콘이 계정 이름 옆에 나타나는 경우 계정에 대한 휴대폰 로그인을 이미 설정했음을 의미합니다. 앱 외부에서 인증 요청에 대한 알림을 받을 수 있도록 계정에 대한 푸시 알림을 추가하라는 메시지가 표시될 수 있습니다.

    - **2단계 인증에 대한 앱을 사용하고 있는 경우** 앱 및 2단계 인증을 이미 사용하고 있는 경우 계정 이름 옆의 드롭다운 화살표를 선택한 다음, **휴대폰 로그인 사용**을 선택할 수 있습니다.
    
    - **계정을 찾을 수 없는 경우** 앱의 **계정** 화면에서 계정을 찾을 수 없는 경우 앱에 계정을 아직 추가하지 않은 것을 의미합니다. [개인 Microsoft 계정 추가](user-help-auth-app-add-personal-ms-account.md#add-your-personal-microsoft-account) 문서의 단계를 수행하여 개인 Microsoft 계정을 추가합니다.

### <a name="sign-in-to-your-account-using-phone-sign-in"></a>휴대폰 로그인을 사용하여 계정에 로그인

1. 개인 Microsoft 계정 로그인 페이지로 이동한 다음, 암호를 입력하는 대신 **Microsoft Authenticator 앱을 대신 사용** 링크를 선택합니다. 

    Microsoft는 사용자의 휴대폰에 알림을 보냅니다. 

2. 알림을 승인합니다. 

## <a name="sign-in-using-two-factor-verification-for-your-account"></a>계정에 2단계 인증을 사용하여 로그인
표준 2단계 인증 방법은 로그인하는 디바이스에 사용자 이름 및 암호를 입력한 다음, Microsoft Authenticator 앱에서 알림을 보낼지, 아니면 Microsoft Authenticator 앱의 **계정** 화면에서 연결된 확인 코드를 복사할지 여부를 선택해야 합니다. Microsoft Authenticator 앱에 계정을 추가하는 프로세스의 일환으로 계정에 대해 2단계 인증을 설정합니다.

>[!Note]
>Microsoft Authenticator 앱의 **계정** 화면에 회사 또는 학교 계정 또는 개인 계정이 표시되지 않는 경우 Microsoft Authenticator 앱에 계정을 추가하지 않은 것을 의미합니다. 계정을 추가하려면 [회사 또는 학교 계정 추가](user-help-auth-app-add-work-school-account.md) 또는 [개인 계정 추가](user-help-auth-app-add-personal-ms-account.md)를 참조하세요.

2단계 인증의 다양한 방법을 사용하여 회사 또는 학교 또는 개인 계정에 로그인하는 데 필요한 단계는 [2단계 인증 또는 보안 정보를 사용하여 로그인](user-help-sign-in.md)을 참조하세요.

## <a name="frequently-asked-questions"></a>질문과 대답
|**질문**|**해결 방법**|
|--------------|-------------|
|**휴대폰에 암호를 입력하는 것보다 안전하게 로그인할 수 있나요?**|오늘날 대부분의 사람들은 사용자 이름 및 암호를 사용하여 웹 사이트 또는 앱에 로그인합니다. 그러나 암호를 분실하거나, 도난당하거나, 해커가 추측할 가능성이 있습니다.<br><br>Microsoft Authenticator 앱을 설정하면 이 앱은 휴대폰의 PIN 또는 생체 인식 잠금으로 보호되는 계정을 잠금 해제하는 키를 휴대폰에 만듭니다. 이 키는 로그인하는 동안 신원을 증명하는 데 사용됩니다.<br><br>**중요**<br>데이터는 키를 로컬로 보호하는 용도로만 사용됩니다. 어떤 경우에도 전송되거나 클라우드에 저장되지 않습니다.|
|**휴대폰 로그인은 2단계 인증을 대체하나요? 이 기능을 꺼야 하나요?**|휴대폰 로그인은 2단계 모두 모바일 디바이스에서 발생하는 2단계 인증의 형식입니다. 계정에 대한 추가 보안을 제공하도록 설정한 2단계 인증을 유지해야 합니다.|
|**내 계정에 대해 2단계 인증을 계속 설정하는 경우에 두 개의 알림을 승인해야 하나요?**| 아니요. 휴대폰을 사용하여 Microsoft 계정에 로그인해도 2단계 인증으로 집계되므로 두 번째 승인은 필요 없습니다.|
|**휴대폰을 분실하거나 휴대하지 않은 경우 계정에 액세스하려면 어떻게 해야 하나요?**| 언제든지 로그인 페이지에서 [암호를 대신 사용]을 선택하여 암호를 사용하도록 전환할 수 있습니다. 그러나 2단계 인증을 사용하더라도 여전히 두 번째 방법을 사용하여 신분을 증명해야 합니다.<br><br>**중요**<br>계정에 두 가지 이상의 최신 인증 방법을 연결하는 것이 좋습니다.<br><br>[보안 설정](https://account.live.com/proofs/manage) 페이지에서 개인 계정의 인증 방법을 관리할 수 있습니다. 회사 또는 학교 계정이면 관리자가 보안 정보를 설정한 경우 조직의 [추가 보안 인증](https://aka.ms/MFASetup) 페이지 또는 **계정 보안 유지** 페이지로 이동하면 됩니다. 보안 정보에 대 한 자세한 내용은 참조 하세요. [보안 정보 (미리 보기) 개요](user-help-security-info-overview.md)합니다.<br><br>인증 방법을 관리할 수 없으면 관리자에게 문의해야 합니다.|
|**이 기능을 중지하고 다시 암호를 사용하려면 어떻게 해야 하나요?**|개인 계정의 경우 로그인하는 동안 **암호를 대신 사용** 링크를 선택합니다. 가장 최근에 사용한 방법이 저장되어 다음에 로그인할 때 기본값으로 제공됩니다. 다시 휴대폰 로그인을 사용하려면 로그인하는 동안 **앱을 대신 사용** 링크를 선택합니다.<br><br>회사 또는 학교 계정에 대 한 중 장치에서의 등록 취소는 **설정** Microsoft Authenticator 앱의 페이지에서 장치를 사용 하지 않도록 설정 하거나 합니다 **장치 및 활동** 프로필의 영역입니다. 프로필에서 장치를 사용 하지 않도록 설정 하는 방법에 대 한 자세한 내용은 참조 하세요. [My Apps 포털에서 프로필 및 계정 정보를 업데이트](my-apps-portal-end-user-update-profile.md#view-your-organization-related-profile-information)합니다.|
|**휴대폰 로그인에 회사 또는 학교 계정을 둘 이상 사용할 수 없는 이유는 무엇인가요?**| 한 휴대폰은 하나의 회사 또는 학교 계정에 등록되어야 합니다. 다른 회사 또는 학교 계정에서 휴대폰 로그인을 사용하려면 먼저 **설정** 페이지를 통해 기존 디바이스의 등록을 취소해야 합니다.|
|**휴대폰을 사용하여 내 컴퓨터에 로그인할 수 있나요?**| 컴퓨터에서 Windows 10의 Windows Hello를 사용하여 로그인하는 것이 좋습니다. Windows Hello는 얼굴, 지문 또는 PIN을 사용하여 로그인할 수 있습니다.|

## <a name="next-steps"></a>다음 단계

- 개인 Microsoft 계정에 대 한 확인 코드를 시작 하는 데 문제가 있는 경우 참조를 **확인 코드 문제 해결** 섹션을 [Microsoft 계정 보안 정보 및 확인 코드](https://support.microsoft.com/en-us/help/12428/microsoft-account-security-info-verification-codes) 문서.

- 앱에 대한 일반적인 질문이 더 있는 경우 [Microsoft Authenticator FAQ](user-help-auth-app-faq.md)를 참조하세요.

- 2단계 인증에 대해 더 자세히 알아보려면 [2단계 인증에 내 계정 설정](multi-factor-authentication-end-user-first-time.md)을 참조하세요.

- 보안 정보에 대 한 자세한 정보를 원한다 면 참조 [보안 정보 (미리 보기) 개요](user-help-security-info-overview.md)
