---
title: 포함 파일
description: 포함 파일
services: iot-accelerators
author: v-krghan
ms.service: iot-accelerators
ms.topic: include
ms.date: 01/25/2019
ms.author: v-krghan
ms.custom: include file
ms.openlocfilehash: 81590a4d686d85482bee38c4391b8ac24b25658e
ms.sourcegitcommit: 2d0fb4f3fc8086d61e2d8e506d5c2b930ba525a7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/18/2019
ms.locfileid: "58114672"
---
## <a name="download-the-source-code"></a>소스 코드 다운로드

원격 모니터링 소스 코드 리포지토리에는 마이크로 서비스 Docker 이미지를 실행하는 데 필요한 소스 코드 및 Docker 구성 파일이 포함되어 있습니다.

리포지토리의 로컬 버전을 복제하고 만들려면 명령줄 환경을 사용하여 로컬 머신의 적절한 폴더로 이동합니다. 그런 다음, 다음 명령 세트 중 하나를 실행하여 java 리포지토리를 복제합니다.

java 마이크로 서비스 구현의 최신 버전을 다운로드하려면 다음을 실행합니다.


```cmd/sh
git clone --recurse-submodules https://github.com/Azure/azure-iot-pcs-remote-monitoring-java.git

# To retrieve the latest submodules, run the following command:

cd azure-iot-pcs-remote-monitoring-java
git submodule foreach git pull origin master
```

> [!NOTE]
> 이러한 명령은 마이크로 서비스를 로컬로 실행하는 데 사용하는 스크립트 외에도 모든 마이크로 서비스에 대한 소스 코드를 다운로드합니다. Docker에서 마이크로 서비스를 실행하는 데는 소스 코드가 필요하지 않지만, 나중에 솔루션 가속기를 수정하고 변경 내용을 로컬로 테스트하려는 경우에는 소스 코드가 유용합니다.

## <a name="deploy-the-azure-services"></a>Azure 서비스 배포

이 문서에서는 마이크로 서비스를 로컬로 실행하는 방법을 보여주지만 클라우드에서 실행되는 Azure 서비스를 사용합니다. 다음 스크립트를 사용하여 Azure 서비스를 배포합니다. 다음 스크립트 예제에서는 Windows 머신에서 java 리포지토리를 사용한다고 가정합니다. 다른 환경에서 작업하는 경우 경로, 파일 확장명 및 경로 구분 기호를 적절하게 조정합니다.

### <a name="create-new-azure-resources"></a>새 Azure 리소스 만들기

아직 필요한 Azure 리소스를 만들지 않은 경우 다음 단계를 수행합니다.

1. 명령줄 환경에서 리포지토리의 복제된 복사본에 있는 **\services\scripts\local\launch** 폴더로 이동합니다.

1. 다음 명령을 실행하여 **pcs** CLI 도구를 설치하고 Azure 계정에 로그인합니다.

    ```cmd
    npm install -g iot-solutions
    pcs login
    ```

1. **start.cmd** 스크립트를 실행합니다. 스크립트에서 다음 정보를 요구하는 메시지가 표시됩니다.
   * 솔루션 이름
   * 사용할 Azure 구독입니다.
   * 사용할 Azure 데이터 센터의 위치

     스크립트는 솔루션 이름을 사용하여 Azure에서 리소스 그룹을 만듭니다. 이 리소스 그룹에는 솔루션 가속기에서 사용하는 Azure 리소스가 포함됩니다. 해당 리소스가 더 이상 필요하지 않으면 이 리소스 그룹을 삭제할 수 있습니다.

     또한 이 스크립트는 로컬 머신에 **PCS** 접두사가 있는 환경 변수 세트도 추가합니다. Docker 컨테이너 또는 마이크로 서비스 프로젝트를 로컬로 시작하면 이러한 환경 변수에서 해당 구성 값을 읽습니다.

     > [!TIP]
     > 스크립트가 완료되면 **\<홈 폴더\>\\.pcs\\\<솔루션 이름\>.env**라는 파일에 환경 변수를 저장합니다. 나중에 솔루션 가속기 배포에 사용할 수 있습니다. **docker-compose**를 실행할 때 로컬 머신에 설정된 모든 환경 변수에서 **services\\scripts\\local\\.env** 파일의 값을 재정의합니다.

1. 명령줄 환경에서 나갑니다.

### <a name="use-existing-azure-resources"></a>기존 Azure 리소스 사용

필요한 Azure 리소스를 이미 만든 경우 로컬 머신에 해당 환경 변수를 만듭니다. 이러한 환경 변수는 배포의 **\<홈 폴더\>\\.pcs\\\<솔루션 이름\>.env** 파일에 저장될 수 있습니다. **docker-compose**를 실행할 때 로컬 머신에 설정된 환경 변수에서 **services\\scripts\\local\\.env** 파일의 값을 재정의합니다.