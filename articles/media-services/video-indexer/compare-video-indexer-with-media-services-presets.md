---
title: Video Indexer와 Azure Media Services v3 미리 설정 비교 | Microsoft Docs
description: 이 항목에서는 Video Indexer와 Azure Media Services v3 미리 설정을 비교합니다.
services: media-services
documentationcenter: ''
author: juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2019
ms.author: juliako
ms.openlocfilehash: b4c74a67c66b12e3a7333f3e679e7c61a750cf7e
ms.sourcegitcommit: e69fc381852ce8615ee318b5f77ae7c6123a744c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56002394"
---
# <a name="compare-azure-media-services-v3-presets-and-video-indexer"></a>Azure Media Services v3 미리 설정 및 Video Indexer 비교 

이 문서에서는 **Video Indexer API**와 **Media Services v3 API**의 기능을 비교합니다. 

현재 [Video Indexer v2 API](https://api-portal.videoindexer.ai/)와 [Media Services v3 API](https://github.com/Azure/azure-rest-api-specs/blob/master/specification/mediaservices/resource-manager/Microsoft.Media/stable/2018-07-01/Encoding.json)에는 중복되는 기능이 있습니다. 다음 표에는 차이점과 유사점을 이해하기 위한 현재의 지침이 나와 있습니다. 

## <a name="compare"></a>비교

|기능|Video Indexer API |Media Services v3 API의<br/>비디오 분석기 및 오디오 분석기 미리 설정|
|---|---|---|
|미디어 인사이트|[향상된 기능](video-indexer-output-json-v2.md) |[기본 사항](../latest/intelligence-concept.md)|
|환경|지원되는 기능의 전체 목록 보기: <br/> [개요](video-indexer-overview.md)|비디오 인사이트만 반환합니다.|
|결제|[Media Services 가격](https://azure.microsoft.com/pricing/details/media-services/#analytics)|[Media Services 가격](https://azure.microsoft.com/pricing/details/media-services/#analytics)|
|규정 준수|[Azure 규정 준수](https://aka.ms/AzureCompliance)|Media Services는 많은 인증을 준수합니다. [Azure Compliance Offerings.pdf](https://gallery.technet.microsoft.com/Overview-of-Azure-c1be3942/file/178110/23/Microsoft%20Azure%20Compliance%20Offerings.pdf)를 살펴보고, "Media Services"를 검색하여 관심 인증서를 준수하는지 확인합니다.|
|평가판|미국 동부|사용할 수 없음|
|가용성 |미국 서부, 동아시아, 북유럽|[Azure 상태](https://azure.microsoft.com/global-infrastructure/services/?products=media-services) 참조|

## <a name="next-steps"></a>다음 단계

[Video Indexer 개요](video-indexer-overview.md)

[Media Services v3 개요](../latest/media-services-overview.md)
