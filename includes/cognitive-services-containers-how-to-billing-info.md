---
author: diberry
ms.author: diberry
ms.service: cognitive-services
ms.topic: include
ms.date: 03/11/2019
ms.openlocfilehash: 200e2dfd2dd4f9aedd9256b307491a0b207ea124
ms.sourcegitcommit: 5839af386c5a2ad46aaaeb90a13065ef94e61e74
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2019
ms.locfileid: "57964214"
---
컨테이너에 대 한 쿼리 사용에 대 한 Azure 리소스의 가격 책정 계층으로 청구를 `<ApiKey>`입니다.

Cognitive Services 컨테이너는 계량에 대 한 청구 끝점에 연결 하지 않고 실행 하는 허가 되지 않습니다. 고객은 항상 청구 끝점을 사용 하 여 청구 정보를 통신 하도록 컨테이너를 사용 하도록 설정 해야 합니다. Cognitive Services 컨테이너는 고객 데이터(예: 분석 중인 이미지 또는 텍스트)를 Microsoft에 보내지 않습니다. 

### <a name="connecting-to-azure"></a>Azure에 연결

컨테이너 실행에 청구 인수 값이 필요 합니다. 이러한 값 컨테이너 청구 끝점에 연결할 수 있습니다. 컨테이너는 약 10 ~ 15분마다 사용량을 보고합니다. 컨테이너를 Azure에 허용 되는 시간 창 내에서 연결 되지 컨테이너는 계속 실행 되지만 청구 끝점 복원 될 때까지 쿼리를 제공 하지 않습니다. 연결을 10 ~ 15 분의 동일한 시간 간격에 10 번 시도 합니다. 10 회 내 청구에 끝점에 연결할 수 없는 경우 컨테이너 실행이 중지 됩니다. 

### <a name="billing-arguments"></a>청구 인수

다음 옵션 중 세 모두에서 유효한 값으로 지정 해야 합니다는 `docker run` 컨테이너를 시작 하는 명령:

| 옵션 | 설명 |
|--------|-------------|
| `ApiKey` | 청구 정보를 추적하는 데 사용되는 Cognitive Service 리소스의 API 키입니다.<br/>이 옵션의 값은 `Billing`에 지정된 프로비저닝된 리소스에 대한 API 키로 설정해야 합니다. |
| `Billing` | 청구 정보를 추적하는 데 사용되는 Cognitive Service 리소스의 엔드포인트입니다.<br/>이 옵션의 값은 프로비전된 LUIS Azure 리소스의 엔드포인트 URI로 설정해야 합니다.|
| `Eula` | 컨테이너에 대한 라이선스에 동의했음을 나타냅니다.<br/>이 옵션의 값은 `accept`로 설정해야 합니다. |


