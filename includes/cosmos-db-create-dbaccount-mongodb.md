---
title: 포함 파일
description: 포함 파일
services: cosmos-db
author: rimman
ms.service: cosmos-db
ms.topic: include
ms.date: 12/26/2018
ms.author: rimman
ms.custom: include file
ms.openlocfilehash: f000f10a3b20fda04c908a6dea0cc9799b49ef76
ms.sourcegitcommit: 7e772d8802f1bc9b5eb20860ae2df96d31908a32
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2019
ms.locfileid: "57457913"
---
1. 새 창에서 [Azure Portal](https://portal.azure.com/)에 로그인합니다.
2. 왼쪽 메뉴에서 **리소스 만들기**, **데이터베이스**를 차례로 클릭한 다음, **Azure Cosmos DB**에서 **만들기**를 클릭합니다.
   
   ![더 많은 서비스와 Azure Cosmos DB를 강조 표시한 Azure Portal의 스크린샷](./media/cosmos-db-create-dbaccount-mongodb/create-nosql-db-databases-json-tutorial-1.png)

3. **Azure Cosmos DB 계정 만들기** 페이지에서 새 Azure Cosmos DB 계정에 대한 설정을 입력합니다. 
 
    설정|값|설명
    ---|---|---
    구독|사용자의 구독|이 Azure Cosmos DB 계정에 사용하려는 Azure 구독을 선택합니다. 
    리소스 그룹|새로 만들기<br><br>다음으로, ID에 제공된 것과 동일한 고유한 이름 입력|**새로 만들기**를 선택합니다. 그런 다음, 계정에 대한 새 리소스 그룹 이름을 입력합니다. 간단히 하기 위해 ID와 동일한 이름을 사용합니다. 
    계정 이름|고유한 이름을 입력합니다.|내 Azure Cosmos DB 계정을 식별하는 고유한 이름을 입력합니다. URI를 만들기 위해 제공하는 ID에 *documents.azure.com*이 추가되므로 고유한 ID를 사용합니다.<br><br>ID는 소문자, 숫자 및 하이픈(-) 문자만 사용할 수 있으며, 3~31자여야 합니다.
    API|Azure Cosmos DB의 API for MongoDB|API는 만들 계정의 형식을 결정합니다. Azure Cosmos DB는 문서 데이터베이스용 Core(SQL), 그래프 데이터베이스용 Gremlin, 문서 데이터베이스용 Azure Cosmos DB의 API MongoDB, Azure Table 및 Cassandra의 5가지 API를 제공합니다. 현재 각 API에 대한 별도의 계정을 만들어야 합니다. <br><br>이 빠른 시작에서는 MongoDB를 사용하는 테이블을 만들 예정이므로 **MongoDB**를 선택합니다.|
    위치|사용자와 가장 가까운 지역 선택|Azure Cosmos DB 계정을 호스트할 지리적 위치를 선택합니다. 데이터에 가장 빨리 액세스할 수 있도록 사용자와 가장 가까운 위치를 사용합니다.

    **검토+만들기**를 선택합니다. **네트워크** 및 **태그** 섹션을 건너뛸 수 있습니다. 

    ![Azure Cosmos DB에 대한 새 계정 페이지](./media/cosmos-db-create-dbaccount-mongodb/azure-cosmos-db-create-new-account.png)

4. 계정 생성에는 몇 분 정도가 소요됩니다. 포털에서 **축하합니다! MongoDB에 대한 유선 프로토콜 호환성이 있는 Cosmos 계정이 준비되었습니다.** 페이지를 표시할 때까지 기다립니다.

    ![Azure Portal 알림 창](./media/cosmos-db-create-dbaccount-mongodb/azure-cosmos-db-account-created.png)
