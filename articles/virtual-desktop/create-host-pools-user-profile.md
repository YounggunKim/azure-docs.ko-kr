---
title: Windows 가상 데스크톱 미리 보기 호스트 풀-Azure에 대 한 사용자 프로필 공유 설정
description: Windows 가상 데스크톱 미리 보기 호스트 풀 FSLogix 프로필 컨테이너를 설정 하는 방법입니다.
services: virtual-desktop
author: Heidilohr
ms.service: virtual-desktop
ms.topic: how-to
ms.date: 03/21/2019
ms.author: helohr
ms.openlocfilehash: c9c2ca2cc27c5fa757b8ff6846e0a6a8f7087875
ms.sourcegitcommit: 81fa781f907405c215073c4e0441f9952fe80fe5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/25/2019
ms.locfileid: "58403717"
---
# <a name="set-up-a-user-profile-share-for-a-host-pool"></a>호스트 풀에 대 한 사용자 프로필 공유 설정

Windows 가상 데스크톱 미리 보기 서비스는 권장 되는 사용자 프로필 솔루션으로 FSLogix 프로필 컨테이너를 제공합니다. 사용자 프로필 디스크 (UPD) 솔루션을 사용 하 여 권장 하지 않습니다 하 고 Windows 가상 데스크톱의 이후 버전에서 사용 되지 않습니다.

이 섹션에서는 호스트 풀에 대 한 FSLogix 프로필 컨테이너 공유를 설정 하는 방법을 알려줍니다.

## <a name="create-a-new-virtual-machine-that-will-act-as-a-file-share"></a>파일 공유로 할 새 가상 머신 만들기

가상 컴퓨터를 만들 때 하거나 동일한 가상 네트워크에 풀 가상 머신과 호스트 또는 호스트 풀 가상 컴퓨터에 연결 되어 있는 가상 네트워크에 배치 해야 합니다. 여러 가지 방법으로 가상 컴퓨터를 만들 수 있습니다.

- [Azure 갤러리 이미지에서 가상 머신 만들기](https://docs.microsoft.com/azure/virtual-machines/windows/quick-create-portal#create-virtual-machine)
- [관리 되는 이미지에서 가상 머신 만들기](https://docs.microsoft.com/azure/virtual-machines/windows/create-vm-generalized-managed)
- [관리 되지 않는 이미지에서 가상 머신 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)

가상 컴퓨터를 만든 후 도메인에 가입 된 다음을 수행 하 여:

1. [가상 머신에 연결](https://docs.microsoft.com/azure/virtual-machines/windows/quick-create-portal#connect-to-virtual-machine) 가상 머신을 만들 때 제공한 자격 증명을 사용 합니다.
2. 가상 컴퓨터에서 시작 **Control Panel** 선택한 **시스템**입니다.
3. 선택 **컴퓨터 이름**를 선택 **설정을 변경**를 선택한 후 **변경 하는 중...**
4. 선택 **도메인** 가상 네트워크에 Active Directory 도메인을 입력 합니다.
5. 도메인 가입 컴퓨터에 대 한 권한이 있는 도메인 계정으로 인증 합니다.

## <a name="prepare-the-virtual-machine-to-act-as-a-file-share-for-user-profiles"></a>사용자 프로필에 대 한 파일 공유로 작동 하도록 가상 머신 준비

사용자 프로필에 대 한 파일 공유로 작동 하도록 가상 컴퓨터를 준비 하는 방법에 대 한 일반 지침은 다음과 같습니다.

1. 세션 호스트 가상 컴퓨터에 연결 된 [Active Directory 보안 그룹](https://docs.microsoft.com/windows/security/identity-protection/access-control/active-directory-security-groups)합니다. 이 보안 그룹 방금 만든 파일 공유 가상 컴퓨터에 세션 호스트 가상 컴퓨터를 인증에 사용 됩니다.
2. [파일 공유 가상 머신에 연결](https://docs.microsoft.com/azure/virtual-machines/windows/quick-create-portal#connect-to-virtual-machine)합니다.
3. 파일 공유 가상 컴퓨터에 폴더를 만들고 합니다 **C 드라이브** 프로 파일 공유로 사용 되는 합니다.
4. 새 폴더를 마우스 오른쪽 단추로 클릭 한 다음를 선택 합니다 **속성**를 선택 **공유**를 선택 하 고 **고급 공유 하는 중...** .
5. 선택 **이 폴더를 공유**, 선택 **권한...** 를 선택 하 고 **추가...** .
6. 세션 호스트 가상 컴퓨터에 추가 된 보안 그룹을 검색 한 다음 해당 그룹에 있는지 **전면적인**합니다.
7. 폴더를 마우스 오른쪽 단추로 클릭는 보안 그룹을 추가한 후을 선택 합니다 **속성**를 선택 **공유**, 아래로 복사 합니다 **네트워크 경로** 나중에 사용할 합니다.

권한에 대 한 모범 사례는 다음을 참조 하세요 [FSLogix 설명서](https://support.fslogix.com/index.php/forum-main/faqs/84-best-practices#120)합니다.

## <a name="configure-the-fslogix-profile-container"></a>FSLogix 프로필 컨테이너 구성

FSLogix 소프트웨어를 사용 하 여 가상 컴퓨터를 구성 하려면 호스트 그룹에 등록 된 각 컴퓨터에서 다음을 수행 합니다.

1. [가상 머신에 연결](https://docs.microsoft.com/azure/virtual-machines/windows/quick-create-portal#connect-to-virtual-machine) 가상 머신을 만들 때 제공한 자격 증명을 사용 합니다.
2. 인터넷 브라우저를 시작 하 고 다음 이동할 [링크](https://go.microsoft.com/fwlink/?linkid=2084562) FSLogix 에이전트를 다운로드 합니다. Windows 가상 데스크톱 공개 미리 보기의 일부로, FSLogix 소프트웨어를 활성화 하려면 라이선스 키를 얻을 수 있습니다. 키는 LicenseKey.txt 파일 FSLogix 에이전트.zip 파일에 포함 합니다.
3. FSLogix 에이전트를 설치 합니다.
4. 이동할 **Program Files** > **FSLogix** > **앱** 에이전트 설치를 확인 합니다.
5. 시작 메뉴에서 실행 **RegEdit** 관리자 권한으로 합니다. 이동할 **컴퓨터\\HKEY_LOCAL_MACHINE\\소프트웨어\\FSLogix\\프로필**
6. 다음 값을 만듭니다.

| 이름                | Type               | 데이터/값                        |
|---------------------|--------------------|-----------------------------------|
| 사용             | DWORD              | 1                                 |
| VHDLocations        | 다중 문자열 값 | "파일 공유에 대 한 네트워크 경로" |
| VolumeType          | 문자열             |  VHDX                              |
| SizeInMBs           | DWORD              | "프로필의 크기에 대 한 정수"     |
| IsDynamic           | DWORD              | 1                                 |
| LockedRetryCount    | DWORD              | 1                                 |
| LockedRetryInterval | DWORD              | 0                                 |
