---
title: FTP 서버-Azure Logic Apps에 연결
description: Azure Logic Apps을 사용하여 FTP 서버에 파일 만들기, 모니터링 및 관리
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: divswa, LADocs
ms.topic: article
ms.date: 10/15/2018
tags: connectors
ms.openlocfilehash: e5aeaa707c7a839483484c524e982204d6fe055c
ms.sourcegitcommit: c63fe69fd624752d04661f56d52ad9d8693e9d56
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2019
ms.locfileid: "58576329"
---
# <a name="create-monitor-and-manage-ftp-files-by-using-azure-logic-apps"></a>Azure Logic Apps를 사용하여 FTP 파일 만들기, 모니터링 및 관리

Azure Logic Apps 및 FTP 커넥터를 사용하면 다음과 같이 다른 작업과 함께 FTP 서버의 계정을 통해 파일을 만들고, 모니터하고, 보내고, 수신하는 자동화된 작업 및 워크플로를 만들 수 있습니다.

* 파일이 추가되거나 변경될 때 모니터링합니다.
* 파일을 가져오고, 만들고, 복사, 업데이트, 나열 및 삭제합니다.
* 파일 콘텐츠 및 메타데이터를 가져옵니다.
* 보관을 폴더로 추출합니다.

트리거를 사용하여 FTP 서버에서 응답을 가져오고 다른 작업에 출력을 제공하는 트리거를 사용할 수 있습니다. Logic Apps의 실행 작업을 사용하여 FTP 서버에 있는 파일을 관리할 수 있습니다. 다른 작업에서 FTP 작업의 출력을 사용하게 만들 수도 있습니다. 예를 들어 정기적으로 FTP 서버에서 파일을 검색하는 경우 Office 365 Outlook 커넥터 또는 Outlook.com 커넥터를 사용하여 해당 파일 및 해당 콘텐츠에 대한 이메일을 보낼 수 있습니다. 논리 앱을 처음 접하는 경우 [Azure Logic Apps란?](../logic-apps/logic-apps-overview.md)을 검토합니다.

## <a name="limits"></a>제한

* FTP 작업 지원 된 파일만 *50MB 또는 더 적게* 사용 하지 않는 경우 [메시지 청크](../logic-apps/logic-apps-handle-large-messages.md),이 제한을 초과할 수 있도록 하 합니다. 현재 FTP 트리거 청크를 지원 하지 않습니다.

* FTP 커넥터만 명시적 FTP를 통해 SSL (FTPS)을 지원 하 고 암시적 FTPS를 사용 하 여 호환 되지 않습니다.

## <a name="prerequisites"></a>필수 조건

* Azure 구독. Azure 구독이 없는 경우 <a href="https://azure.microsoft.com/free/" target="_blank">체험 Azure 계정에 등록</a>합니다. 

* FTP 호스트 서버 주소 및 계정 자격 증명

  FTP 커넥터를 사용하려면 인터넷에서 액세스할 수 있고 *passive* 모드로 작동하도록 설정된 FTP 서버가 필요합니다. 자격 증명이 있으면 논리 앱에서 연결을 만들고 FTP 계정에 액세스할 수 있습니다.

* [논리 앱 만드는 방법](../logic-apps/quickstart-create-first-logic-app-workflow.md)에 관한 기본 지식

* FTP 계정에 액세스하려는 논리 앱입니다. FTP 트리거를 시작하려면 [빈 논리 앱을 만듭니다](../logic-apps/quickstart-create-first-logic-app-workflow.md). FTP 동작을 사용하려면 예를 들어 **되풀이** 트리거 같은 다른 트리거를 통해 논리 앱을 시작합니다.

## <a name="connect-to-ftp"></a>FTP에 연결

[!INCLUDE [Create connection general intro](../../includes/connectors-create-connection-general-intro.md)]

1. [Azure Portal](https://portal.azure.com)에 로그인하고, 아직 열리지 않은 경우 Logic App Designer에서 논리 앱을 엽니다.

1. 빈 논리 앱의 경우 검색 상자에서 필터로 “ftp”를 입력합니다. 트리거 목록에서 원하는 트리거를 선택합니다.

   또는

   기존 논리 앱의 경우 작업을 추가하려는 마지막 단계에서 **새 단계**를 선택한 다음, **작업 추가**를 선택합니다. 
   검색 상자에서 필터로 "ftp"를 입력합니다. 
   작업 목록에서 원하는 작업을 선택합니다.

   단계 사이에서 작업을 추가하려면 단계 사이에 있는 화살표 위로 포인터를 이동합니다. 
   표시되는 더하기 기호(**+**)를 선택한 다음, **작업 추가**를 선택합니다.

1. 연결에 필요한 세부 정보를 입력한 다음, **만들기**를 선택합니다.

1. 선택한 트리거 또는 작업에 대해 필요한 세부 정보를 제공하고 논리 앱의 워크플로를 계속 빌드합니다.

파일 콘텐츠를 요청하는 경우 트리거는 50MB보다 큰 파일을 가져오지 않습니다. 50MB보다 큰 파일을 가져오려면 다음 패턴을 따릅니다.

* **파일이 추가되거나 수정된 경우(메타데이터만)** 등의 파일 속성을 반환하는 트리거를 사용합니다.

* 트리거에서 **경로를 사용하여 파일 콘텐츠 가져오기**와 같이 전체 파일을 읽는 작업을 수행하고, 작업에서 [메시지 청크 분할](../logic-apps/logic-apps-handle-large-messages.md)을 사용하도록 합니다.

## <a name="examples"></a>예

<a name="file-added-modified"></a>

### <a name="ftp-trigger-when-a-file-is-added-or-modified"></a>FTP 트리거: 파일을 추가하거나 수정할 때

이 트리거는 FTP 서버에서 파일이 추가되거나 변경되는 것을 트리거가 감지하면 논리 앱 워크플로를 시작합니다. 따라서 예를 들어 해당 콘텐츠가 지정된 조건을 충족하는지 여부에 따라 파일의 콘텐츠를 확인하고 해당 콘텐츠를 가져올 것인지를 결정하는 조건을 추가할 수 있습니다. 마지막으로 파일의 콘텐츠를 가져오는 작업을 추가하고 해당 콘텐츠를 SFTP 서버의 폴더에 넣을 수 있습니다. 

**엔터프라이즈 예제**: 이 트리거를 사용하여 고객의 주문을 설명하는 새 파일용 FTP 폴더를 모니터링할 수 있습니다. 그런 다음, **파일 콘텐츠 가져오기** 같은 FTP 작업을 사용할 수 있으므로 추가로 처리할 주문의 콘텐츠를 가져오고 주문 데이터베이스에 해당 주문을 저장할 수 있습니다.

파일 콘텐츠를 요청할 경우 트리거 가져올 수 없습니다 파일 50MB 보다 큰. 50MB보다 큰 파일을 가져오려면 다음 패턴을 따릅니다. 

* **파일이 추가되거나 수정된 경우(메타데이터만)** 등의 파일 속성을 반환하는 트리거를 사용합니다.

* 트리거에서 **경로를 사용하여 파일 콘텐츠 가져오기**와 같이 전체 파일을 읽는 작업을 수행하고, 작업에서 [메시지 청크 분할](../logic-apps/logic-apps-handle-large-messages.md)을 사용하도록 합니다.

논리 앱이 유효하고 정상적으로 작동하려면 트리거와 하나 이상의 작업이 필요합니다. 따라서 트리거를 추가한 후 작업을 추가해야 합니다.

이 트리거를 보여 주는 예제는 다음과 같습니다. **파일을 추가하거나 수정할 때**

1. [Azure Portal](https://portal.azure.com)에 로그인하고, 아직 열리지 않은 경우 Logic App Designer에서 논리 앱을 엽니다.

1. 빈 논리 앱의 경우 검색 상자에서 필터로 “ftp”를 입력합니다. 트리거 목록에서 다음 트리거를 선택합니다. **파일을 추가하거나 수정할 때 - FTP**

   ![FTP 트리거를 찾아서 선택](./media/connectors-create-api-ftp/select-ftp-trigger.png)  

1. 연결에 필요한 세부 정보를 입력한 다음, **만들기**를 선택합니다.

   기본적으로 이 커넥터는 파일을 텍스트 형식으로 전송합니다. 
   예를 들어 파일을 이진 형식으로 전송하려면 인코딩을 사용하는 경우에 **이진 전송**을 선택합니다.

   ![FTP 서버 연결 만들기](./media/connectors-create-api-ftp/create-ftp-connection-trigger.png)  

1. **폴더** 상자 옆에서 폴더 아이콘을 선택하여 목록을 표시합니다. 새 파일 또는 편집된 파일에 대해 모니터링할 폴더를 찾으려면 오른쪽 화살표(**>**)를 선택한 다음, 해당 폴더를 찾아서 선택합니다.

   ![모니터링할 폴더를 찾아서 선택](./media/connectors-create-api-ftp/select-folder.png)  

   선택한 폴더가 **폴더** 상자에 나타납니다.

   ![선택한 폴더](./media/connectors-create-api-ftp/selected-folder.png)  

이제 논리 앱에 트리거가 있으니, 논리 앱이 새 파일 또는 편집된 파일을 찾았을 때 실행할 작업을 추가합니다. 이 예제에서는 새 콘텐츠 또는 업데이트된 콘텐츠를 가져오는 FTP 작업을 추가할 수 있습니다.

<a name="get-content"></a>

### <a name="ftp-action-get-content"></a>FTP 작업: 콘텐츠 가져오기

이 작업은 파일이 추가 또는 업데이트되면 FTP 서버의 파일에서 콘텐츠를 가져옵니다. 예를 들어 이전 예제의 트리거 그리고 파일이 추가 또는 편집된 후 해당 파일의 콘텐츠를 가져오는 작업을 추가할 수 있습니다. 

파일 콘텐츠를 요청할 경우 트리거 가져올 수 없습니다 파일 50MB 보다 큰. 50MB보다 큰 파일을 가져오려면 다음 패턴을 따릅니다. 

* **파일이 추가되거나 수정된 경우(메타데이터만)** 등의 파일 속성을 반환하는 트리거를 사용합니다.

* 트리거에서 **경로를 사용하여 파일 콘텐츠 가져오기**와 같이 전체 파일을 읽는 작업을 수행하고, 작업에서 [메시지 청크 분할](../logic-apps/logic-apps-handle-large-messages.md)을 사용하도록 합니다.

다음은 **콘텐츠 가져오기** 작업을 보여 주는 예입니다.

1. 트리거 또는 다른 작업에서 **새 단계**를 선택합니다. 

1. 검색 상자에서 필터로 "ftp"를 입력합니다. 작업 목록에서 다음 작업을 선택합니다. **파일 콘텐츠 가져오기 - FTP**

   ![FTP 작업 선택](./media/connectors-create-api-ftp/select-ftp-action.png)  

1. FTP 서버 및 계정에 대한 연결이 이미 있는 경우 다음 단계로 이동합니다. 그렇지 않은 경우 해당 연결에 필요한 세부 정보를 입력하고 **만들기**를 선택합니다. 

   ![FTP 서버 연결 만들기](./media/connectors-create-api-ftp/create-ftp-connection-action.png)

1. **파일 콘텐츠 가져오기** 작업이 열리면 **파일** 상자 내부를 클릭하여 동적 콘텐츠 목록을 표시합니다. 이제 이전 단계의 출력에 대한 속성을 선택할 수 있습니다. 동적 콘텐츠 목록에서 **파일 콘텐츠** 속성을 선택합니다. 이 속성에는 추가 또는 업데이트된 파일의 콘텐츠가 포함되어 있습니다.  

   ![파일을 찾아서 선택](./media/connectors-create-api-ftp/ftp-action-get-file-content.png)

   이제 **파일 콘텐츠** 속성이 **파일** 상자에 나타납니다.

   ![선택한 "파일 콘텐츠" 속성](./media/connectors-create-api-ftp/ftp-action-selected-file-content-property.png)

1. 논리 앱을 저장합니다. 워크플로를 테스트하려면 현재 논리 앱에서 모니터링하는 FTP 폴더에 파일을 추가합니다.

## <a name="connector-reference"></a>커넥터 참조

커넥터의 openapi 설명 되어 있는 트리거와 작업을 제한 하는 방법에 대 한 기술 정보 (이전의 Swagger) 설명을 검토 합니다 [커넥터의 참조 페이지](/connectors/ftpconnector/)합니다.

## <a name="get-support"></a>지원 받기

* 질문이 있는 경우 [Azure Logic Apps 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)을 방문해 보세요.
* 기능 아이디어를 제출하거나 투표하려면 [Logic Apps 사용자 의견 사이트](https://aka.ms/logicapps-wish)를 방문하세요.

## <a name="next-steps"></a>다음 단계

* 다른 [Logic Apps 커넥터](../connectors/apis-list.md)에 대해 알아봅니다.
