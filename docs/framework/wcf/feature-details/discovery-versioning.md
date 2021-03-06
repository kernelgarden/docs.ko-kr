---
title: "검색 버전 관리"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f91c6d0a-3af2-45c5-9a5c-e75390619836
caps.latest.revision: "10"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: d9a332e9b0aeec74a8cfd87622ce3be7bbffe3c9
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2017
---
# <a name="discovery-versioning"></a>검색 버전 관리
이 항목에서는 일부 새 검색 기능의 구현에 대해 간략하게 설명하고 사용할 검색 버전을 선택하는 방법에 대해서도 간략하게 설명합니다.  
  
## <a name="discovery-versioning"></a>검색 버전 관리  
 검색 기능은 세 가지 버전의 WS_Discovery 프로토콜을 지원합니다. 검색 API를 사용하면 사용할 프로토콜 버전을 선택할 수 있습니다. 이 문서에서는 버전 관리 관련 설정에 대해 간략하게 설명합니다.  
  
 다음은 <xref:System.ServiceModel.Discovery.DiscoveryVersion> 속성을 포함하고 있고 해당 생성자에 <xref:System.ServiceModel.Discovery.DiscoveryVersion> 인수를 사용하는 검색 클래스입니다.  
  
-   <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>  
  
-   <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>  
  
-   <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>  
  
-   <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>  
  
### <a name="discoveryversionwsdiscoveryapril2005"></a>DiscoveryVersion.WSDiscoveryApril2005  
 제공 <xref:System.ServiceModel.Discovery.DiscoveryVersion.WSDiscoveryApril2005> 생성자로 매개 변수는 Ws-discovery 프로토콜의 April2005 버전을 사용 하 여 구현 합니다. 이 버전은 WS-Discovery 프로토콜 사양의 게시된 버전에 해당합니다. WS-Discovery의 April2005 버전을 사용하는 레거시 응용 프로그램과 상호 운용하려면 이 버전을 사용해야 합니다.  
  
### <a name="discoveryversionwsdiscovery11"></a>DiscoveryVersion.WSDiscovery11  
 Api에서 사용 하는 기본 검색 버전은 <xref:System.ServiceModel.Discovery.DiscoveryVersion.WSDiscovery11>합니다. 이 버전은 WS-Discovery 프로토콜의 현재 표준화된 버전입니다.  
  
## <a name="discoveryversionwsdiscoverycd1"></a>DiscoveryVersion.WSDiscoveryCD1  
 <xref:System.ServiceModel.Discovery.DiscoveryVersion.WSDiscoveryCD1>을 생성자 매개 변수로 제공하면 구현 시 WS-Discovery 프로토콜의 committee draft 1 버전이 사용됩니다. WS-Discovery 프로토콜의 CD1 버전을 실행하는 구현과 상호 운용하려면 이 버전의 프로토콜을 사용해야 합니다.  
  
## <a name="supporting-multiple-udp-discovery-endpoints-for-different-discovery-versions-on-a-single-service-host"></a>단일 서비스 호스트에서 다양한 검색 버전에 대해 여러 개의 UDP 검색 끝점 지원  
 단일 서비스 호스트에서 다양한 검색 버전에 대해 여러 개의 UDP 검색 끝점을 노출할 수 있습니다. 이렇게 하려면 각 UDP 검색 끝점에 고유한 주소를 지정해야 합니다. 다음 예제에서는 이 작업을 수행하는 방법을 보여 줍니다.  
  
```  
UdpDiscoveryEndpoint newVersionUdpEndpoint = new UdpDiscoveryEndpoint(DiscoveryVersion.WSDiscovery11);  
UdpDiscoveryEndpoint oldVersionUdpEndpoint = new UdpDiscoveryEndpoint(DiscoveryVersion.WSDiscoveryApril2005);  
  
newVersionUdpEndpoint.Address = new EndpointAddress(newVersionUdpEndpoint.Address.Uri.ToString() + "/version11");  
oldVersionUdpEndpoint.Address = new EndpointAddress(oldVersionUdpEndpoint.Address.Uri.ToString() + "/versionAril2005");  
  
serviceHost.AddServiceEndpoint(newVersionUdpEndpoint);  
serviceHost.AddServiceEndpoint(oldVersionUdpEndpoint);  
```
