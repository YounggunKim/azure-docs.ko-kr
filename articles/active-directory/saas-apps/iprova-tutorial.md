---
title: '자습서: iProva와 Azure Active Directory 통합 | Microsoft Docs'
description: Azure Active Directory와 iProva 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.reviewer: barbkess
ms.assetid: 1eaeef9b-4479-4a9f-b1b2-bc13b857c75c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 12/24/2018
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 395d3887e35d6e9c043d4d947b605e71eb58bd6b
ms.sourcegitcommit: 5839af386c5a2ad46aaaeb90a13065ef94e61e74
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2019
ms.locfileid: "57897336"
---
# <a name="tutorial-azure-active-directory-integration-with-iprova"></a>자습서: iProva와 Azure Active Directory 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 iProva를 통합하는 방법을 알아봅니다.
iProva를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.

* iProva에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.
* 사용자가 자신의 Azure AD 계정으로 iProva에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.

Azure AD와의 SaaS(Software as a Service) 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 애플리케이션 액세스 및 Single Sign-On](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)을 참조하세요.
Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.

## <a name="prerequisites"></a>필수 조건

iProva와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.

* Azure AD 구독 Azure AD 환경이 없으면[Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/) 웹 사이트에서 1개월 평가판을 구할 수 있습니다.
* iProva SSO가 설정된 구독

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

* iProva가 SP에서 시작된 SSO를 지원합니다.

## <a name="add-iprova-from-the-gallery"></a>갤러리에서 iProva 추가

iProva가 Azure AD에 통합되도록 구성하려면 갤러리의 iProva를 관리형 SaaS 앱 목록에 추가합니다.

갤러리에서 iProva를 추가하려면 다음 단계를 수행합니다.

1. [Azure Portal](https://portal.azure.com)의 왼쪽 창에서 **Azure Active Directory**를 선택합니다.

    ![Azure Active Directory 단추](common/select-azuread.png)

2. **엔터프라이즈 애플리케이션**으로 이동한 다음, **모든 애플리케이션**을 선택합니다.

    ![엔터프라이즈 애플리케이션 블레이드](common/enterprise-applications.png)

3. 새 애플리케이션을 추가하려면 대화 상자 맨 위 있는 **새 애플리케이션**을 선택합니다.

    ![새 애플리케이션 단추](common/add-new-app.png)

4. 검색 상자에 **iProva**를 입력합니다. 결과 패널에서 **iProva**를 선택한 다음, **추가**를 선택하여 애플리케이션을 추가합니다.

     ![결과 목록의 iProva](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트

이 섹션에서는 Britta Simon이라는 테스트 사용자를 기반으로 iProva에서 Azure AD Single Sign-On을 구성하고 테스트합니다.
Single Sign-On이 작동하려면 Azure AD 사용자와 iProva의 관련 사용자 간에 연결 관계를 설정해야 합니다.

iProva에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료합니다.

- [iProva에서 구성 정보 검색](#retrieve-configuration-information-from-iprova) - 다음 단계를 위한 준비입니다.
- [Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on) - 사용자가 이 기능을 사용할 수 있도록 합니다.
- [iProva Single Sign-On 구성](#configure-iprova-single-sign-on) - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
- [Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user) - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.
- [Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user) - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.
- [iProva 테스트 사용자 만들기](#create-an-iprova-test-user) - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 iProva에 만듭니다.
- [Single Sign-on 테스트](#test-single-sign-on) - 구성이 작동하는지 여부를 확인합니다.

### <a name="retrieve-configuration-information-from-iprova"></a>iProva에서 구성 정보 검색

이 섹션에서는 iProva에서 정보를 검색하여 Azure AD Single Sign-On을 구성합니다.

1. 웹 브라우저를 열고 다음 URL 패턴을 사용하여 iProva의 **SAML2 정보 페이지**로 이동합니다.

    | | |
    |-|-|
    | `https://SUBDOMAIN.iprova.nl/saml2info`|
    | `https://SUBDOMAIN.iprova.be/saml2info`|
    | | |

     ![iProva SAML2 정보 페이지 보기](media/iprova-tutorial/iprova-saml2-info.png)

2. 다른 브라우저 탭에서 다음 단계를 진행하는 동안 브라우저 탭을 열어 둡니다.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정합니다.

iProva에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.

1. [Azure Portal](https://portal.azure.com/)의 **iProva** 애플리케이션 통합 페이지에서 **Single Sign-On**을 선택합니다.

    ![Single Sign-On 구성 링크](common/select-sso.png)

2. **Single Sign-On 방법 선택** 대화 상자에서 **SAML/WS-Fed** 모드를 선택하여 Single Sign-On을 사용하도록 설정합니다.

    ![Single Sign-On 선택 모드](common/select-saml-option.png)

3. **SAML로 Single Sign-On 설정** 페이지에서 **편집** 아이콘을 선택하여 **기본 SAML 구성** 대화 상자를 엽니다.

    ![기본 SAML 구성의 편집 아이콘](common/edit-urls.png)

4. **기본 SAML 구성** 섹션에서 다음 단계를 수행합니다.

    a. **식별자** 상자를 **iProva SAML2 정보** 페이지의 **EntityID** 레이블 뒤에 표시된 값으로 채웁니다. 이 페이지는 다른 브라우저 탭에서 계속 열려 있습니다.

    b. **회신 URL** 상자를 **iProva SAML2 정보** 페이지의 **회신 URL** 레이블 뒤에 표시된 값으로 채웁니다. 이 페이지는 다른 브라우저 탭에서 계속 열려 있습니다.

    다. **로그온 URL** 상자를 **iProva SAML2 정보** 페이지의 **로그온 URL** 레이블 뒤에 표시된 값으로 채웁니다. 이 페이지는 다른 브라우저 탭에서 계속 열려 있습니다.

    ![iProva 도메인 및 URL Single Sign-On 정보](common/sp-identifier-reply.png)

5. iProva 애플리케이션에는 특정 형식의 SAML 어설션이 필요합니다. 이 애플리케이션에 대해 다음 클레임을 구성합니다. 애플리케이션 통합 페이지의 **사용자 특성** 섹션에서 이러한 특성의 값을 관리할 수 있습니다. **SAML로 Single Sign-On 설정** 페이지에서 **편집** 아이콘을 선택하여 **사용자 특성** 대화 상자를 엽니다.

    ![사용자 특성 대화 상자](common/edit-attribute.png)

6. **사용자 특성** 대화 상자의 **사용자 클레임** 섹션에서 이전 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성합니다. 다음 단계를 수행합니다.

    | Name | 원본 특성| 네임스페이스 |
    | ---------------| -------- | -----|
    | `samaccountname` | `user.onpremisessamaccountname`| `http://schemas.xmlsoap.org/ws/2005/05/identity/claims`|
    | | |

    a. **새 클레임 추가**를 선택하여 **사용자 클레임 관리** 대화 상자를 엽니다.

    ![사용자 클레임](common/new-save-attribute.png)

    ![[사용자 클레임 관리] 대화 상자](common/new-attribute-details.png)

    b. **이름** 상자에서 해당 행에 표시된 특성 이름을 입력합니다.

    다. **네임스페이스** 목록에서 해당 행에 표시되는 네임스페이스 값을 입력합니다.

    d. **원본** 옵션을 **특성**으로 선택합니다.

    e. **원본 특성** 목록에서 해당 행에 표시된 특성 값을 입력합니다.

    f. **확인**을 선택합니다.

    g. **저장**을 선택합니다.

7. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **복사** 아이콘을 선택하여 **앱 페더레이션 메타데이터 URL**을 복사하고 컴퓨터에 저장합니다.

    ![인증서 다운로드 링크](common/copy-metadataurl.png)

### <a name="configure-iprova-single-sign-on"></a>iProva Single Sign-On 구성

1. **관리자** 계정을 사용하여 iProva에 로그인합니다.

2. **이동** 메뉴를 엽니다.

3. **애플리케이션 관리**를 선택합니다.

4. **시스템 설정** 패널에서 **일반**을 선택합니다.

5. **편집**을 선택합니다.

6. **액세스 제어**까지 아래로 스크롤합니다.

    ![iProva 액세스 제어 설정](media/iprova-tutorial/iprova-accesscontrol.png)

7. **Users are automatically logged on with their network accounts**(사용자가 자신의 네트워크 계정으로 자동 로그인됨) 설정을 찾아서 **Yes, authentication via SAML**(예, SAML을 통한 인증)로 변경합니다. 추가 옵션이 표시됩니다.

8. **설정**을 선택합니다.

9. **다음**을 선택합니다.

10. 페더레이션 데이터를 URL에서 다운로드할지 아니면 파일에서 업로드할지 묻는 메시지가 iProva에 표시됩니다. **URL에서** 옵션을 선택합니다.

    ![Azure AD 메타데이터 다운로드](media/iprova-tutorial/iprova-download-metadata.png)

11. “Azure AD Single Sign-On 구성” 섹션의 마지막 단계에서 저장한 메타데이터 URL을 붙여넣습니다.

12. 화살표 모양의 단추를 선택하여 Azure AD에서 메타데이터를 다운로드합니다.

13. 다운로드가 완료되면 확인 메시지, **Valid Federation Data file downloaded**(유효한 페더레이션 데이터 파일이 다운로드됨)가 표시됩니다.

14. **다음**을 선택합니다.

15. **Test login**(로그인 테스트) 옵션은 건너뛰고 **다음**을 선택합니다.

16. **Claim to use**(사용할 클레임) 드롭다운에서 **windowsaccountname**을 선택합니다.

17. **마침**을 선택합니다.

18. 이제 **Edit general settings**(일반 설정 편집) 화면으로 돌아갑니다. 페이지 맨 아래까지 아래로 스크롤하고 **확인**을 선택하여 구성을 저장합니다.

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기

이 섹션에서는 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만듭니다.

1. Azure Portal의 왼쪽 창에서 **Azure Active Directory** > **사용자** > **모든 사용자**를 선택합니다.

    ![사용자 및 그룹과 모든 사용자 링크](common/users.png)

2. 화면 위쪽에서 **새 사용자**를 선택합니다.

    ![새 사용자 단추](common/new-user.png)

3. **사용자** 대화 상자에서 다음 단계를 수행합니다.

    ![사용자 대화 상자](common/user-properties.png)

    a. **이름** 상자에 **BrittaSimon**과 같은 입력합니다.
  
    b. **사용자 이름** 상자에 *yourname\@yourcompanydomain.extension*을 입력합니다. 
    예는 BrittaSimon@contoso.com입니다.

    다. **암호 표시** 확인란을 선택한 다음, **암호** 상자에 표시된 값을 적어둡니다.

    d. **만들기**를 선택합니다.

### <a name="assign-the-azure-ad-test-user"></a>Azure AD 테스트 사용자 할당

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 iProva에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** > **모든 애플리케이션** > **iProva**를 선택합니다.

    ![엔터프라이즈 애플리케이션 블레이드](common/enterprise-applications.png)

2. 애플리케이션 목록에서 **iProva**를 선택합니다.

    ![애플리케이션 목록의 iProva 링크](common/all-applications.png)

3. 왼쪽 메뉴에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 및 그룹 링크](common/users-groups-blade.png)

4. **사용자 추가**를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![[할당 추가] 대화 상자](common/add-assign-user.png)

5. **사용자 및 그룹** 대화 상자의 **사용자** 목록에서 **Britta Simon**을 선택하고 화면 아래쪽에서 **선택**을 선택합니다.

6. SAML 어설션에 역할 값이 필요한 경우 **역할 선택** 대화 상자에서, 목록에 있는 사용자에게 적절한 역할을 선택합니다. 화면 하단에서 **선택**을 선택합니다.

7. **할당 추가** 대화 상자에서 **할당**을 선택합니다.

### <a name="create-an-iprova-test-user"></a>iProva 테스트 사용자 만들기

1. **관리자** 계정을 사용하여 iProva에 로그인합니다.

2. **이동** 메뉴를 엽니다.

3. **애플리케이션 관리**를 선택합니다.

4. **사용자 및 사용자 그룹** 패널에서 **사용자**를 선택합니다.

5. **추가**를 선택합니다.

6. **사용자 이름** 상자에 *brittasimon\@yourcompanydomain.extension*을 입력합니다. 
    예는 BrittaSimon@contoso.com입니다.

7. **전체 이름** 상자에 **BrittaSimon**과 같은 전체 이름을 입력합니다.

8. **암호 없음(Single Sign-On 사용)** 옵션을 선택합니다.

9. **이메일 주소** 상자에 *yourname\@yourcompanydomain.extension*을 입력합니다. 
   예는 BrittaSimon@contoso.com입니다.

10. 페이지 끝까지 아래로 스크롤하여 **마침**을 선택합니다.

### <a name="test-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.

액세스 패널에서 iProva 타일을 선택하면 SSO를 설정한 iProva에 자동으로 로그인되어야 합니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)를 참조하세요.

## <a name="additional-resources"></a>추가 리소스

- [Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)
- [Azure Active Directory로 애플리케이션 액세스 및 Single Sign-On을 구현하는 방법](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)
- [Azure Active Directory의 조건부 액세스란?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [iProva - SAML2 Single Sign-On을 구성하는 방법](https://webshare.iprova.nl/0wqwm45yn09f5poh/Document.aspx)
