---
title: "방법: Serialize된 데이터 청크 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "이진 serialization, 데이터 청크"
  - "이진 serialization, 예제"
  - "serialize된 데이터 청크"
  - "데이터 청크"
  - "큰 데이터 집합 청크"
  - "serialization, 데이터 청크"
  - "serialization, 예제"
ms.assetid: 22f1b818-7e0d-428a-8680-f17d6ebdd185
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 방법: Serialize된 데이터 청크
대용량 데이터 집합을 웹 서비스 메시지에서 전송할 때 발생하는 두 가지 문제는 다음과 같습니다.  
  
1.  serialization 엔진의 버퍼링으로 인한 대용량 작업 집합\(메모리\)  
  
2.  Base64 인코딩 후 33퍼센트 확장으로 인한 과도한 대역폭 소비  
  
 이러한 문제를 해결하려면 <xref:System.Xml.Serialization.IXmlSerializable> 인터페이스를 구현하여 serialization과 deserialization을 제어합니다.특히 <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A> 및 <xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A> 메서드를 구현하여 데이터를 청크합니다.  
  
### 서버 측 청크를 구현하려면  
  
1.  서버 시스템에서 웹 메서드는 ASP.NET 버퍼링을 끄고 <xref:System.Xml.Serialization.IXmlSerializable>을 구현하는 형식을 반환해야 합니다.  
  
2.  <xref:System.Xml.Serialization.IXmlSerializable>을 구현하는 형식이 <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A> 메서드의 데이터를 청크합니다.  
  
### 클라이언트 측 처리를 구현하려면  
  
1.  클라이언트 프록시에서 웹 메서드를 변경하여 <xref:System.Xml.Serialization.IXmlSerializable>을 구현하는 형식을 반환합니다.<xref:System.Xml.Serialization.Advanced.SchemaImporterExtension>을 사용하여 이 작업을 자동으로 수행할 수 있지만 여기에서는 다루지 않습니다.  
  
2.  <xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A> 메서드를 구현하여 청크된 데이터 스트림을 읽고 바이트를 디스크에 씁니다.또한 이 구현은 진행률 표시줄 등과 같은 그래픽 컨트롤에서 사용할 수 있는 진행률 이벤트도 발생시킵니다.  
  
## 예제  
 다음 코드 예제에서는 ASP.NET 버퍼링을 끄는 클라이언트의 웹 메서드를 보여 줍니다.또한 <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A> 메서드의 데이터를 청크하는 <xref:System.Xml.Serialization.IXmlSerializable> 인터페이스의 클라이언트 측 구현도 보여 줍니다.  
  
 [!code-csharp[HowToChunkSerializedData#1](../../../samples/snippets/csharp/VS_Snippets_Remoting/HowToChunkSerializedData/CS/SerializationChunk.cs#1)]
 [!code-vb[HowToChunkSerializedData#1](../../../samples/snippets/visualbasic/VS_Snippets_Remoting/HowToChunkSerializedData/VB/SerializationChunk.vb#1)]  
[!code-csharp[HowToChunkSerializedData#2](../../../samples/snippets/csharp/VS_Snippets_Remoting/HowToChunkSerializedData/CS/SerializationChunk.cs#2)]
[!code-vb[HowToChunkSerializedData#2](../../../samples/snippets/visualbasic/VS_Snippets_Remoting/HowToChunkSerializedData/VB/SerializationChunk.vb#2)]  
[!code-csharp[HowToChunkSerializedData#3](../../../samples/snippets/csharp/VS_Snippets_Remoting/HowToChunkSerializedData/CS/SerializationChunk.cs#3)]
[!code-vb[HowToChunkSerializedData#3](../../../samples/snippets/visualbasic/VS_Snippets_Remoting/HowToChunkSerializedData/VB/SerializationChunk.vb#3)]  
  
## 코드 컴파일  
  
-   코드에서는 <xref:System>, <xref:System.Runtime.Serialization>, <xref:System.Web.Services>, <xref:System.Web.Services.Protocols>, <xref:System.Xml>, <xref:System.Xml.Serialization> 및 <xref:System.Xml.Schema> 네임스페이스를 사용합니다.  
  
## 참고 항목  
 [사용자 지정 Serialization](../../../docs/framework/serialization/custom-serialization.md)