---
title: "배열 문제 해결 (Visual Basic) | Microsoft 문서"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- troubleshooting arrays
- arrays [Visual Basic], initialization errors
- troubleshooting Visual Basic, arrays
- arrays [Visual Basic], compilation errors
- arrays [Visual Basic], declaration errors
- arrays [Visual Basic], troubleshooting
ms.assetid: f4e971c7-c0a4-4ed7-a77a-8d71039f266f
caps.latest.revision: 17
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: db38c0c2a4f8b74a6b862f86f426b4d8837f4424
ms.lasthandoff: 03/13/2017

---
# <a name="troubleshooting-arrays-visual-basic"></a>배열 문제 해결(Visual Basic)
이 페이지는 배열을 사용할 때 발생할 수 있는 몇 가지 일반적인 문제를 나열 합니다.  
  
## <a name="compilation-errors-declaring-and-initializing-an-array"></a>컴파일 오류를 선언 하 고 배열을 초기화 합니다.  
 선언, 만들기 및 배열 초기화에 대 한 오해에서 컴파일 오류가 발생할 수 있습니다. 오류의 가장 일반적인 원인은 다음과 같습니다.  
  
-   제공 된 [New 연산자](../../../../visual-basic/language-reference/operators/new-operator.md) 차원 길이 지정 하는 배열 변수 선언 뒤에 절. 다음 코드 줄에는 이러한 종류의 잘못 된 선언을 보여 줍니다.  
  
     `Dim INVALIDsingleDimByteArray(2) As Byte = New Byte()`  
  
     `Dim INVALIDtwoDimShortArray(1, 1) As Short = New Short(,)`  
  
     `Dim INVALIDjaggedByteArray(1)() As Byte = New Byte()()`  
  
-   가변 배열의 최상위 배열 보다 차원 길이 지정 합니다. 다음 코드 줄에는 이러한 종류의 잘못 된 선언을 보여 줍니다.  
  
     `Dim INVALIDjaggedByteArray(1)(1) As Byte`  
  
-   생략 된 `New` 키워드 요소 값을 지정 하는 경우. 다음 코드 줄에는 이러한 종류의 잘못 된 선언을 보여 줍니다.  
  
     `Dim INVALIDoneDimShortArray() As Short = Short() {0, 1, 2, 3}`  
  
-   제공 된 `New` 괄호 없이 절 (`{}`). 다음 코드 줄에는 이러한 종류의 잘못 된 선언을 보여 줍니다.  
  
     `Dim INVALIDsingleDimByteArray() As Byte = New Byte()`  
  
     `Dim INVALIDsingleDimByteArray() As Byte = New Byte(2)`  
  
     `Dim INVALIDtwoDimShortArray(,) As Short = New Short(,)`  
  
     `Dim INVALIDtwoDimShortArray(,) As Short = New Short(1, 1)`  
  
## <a name="accessing-an-array-out-of-bounds"></a>범위 밖으로 배열 액세스  
 배열을 초기화 하는 프로세스 각 차원에는 상한값 및 하한값을 할당 합니다. 배열의 요소에 대 한 모든 액세스는 유효한 인덱스 또는 모든 차원에 대해 아래 첨자를 지정 해야 합니다. 모든 인덱스는 하한값 아래 또는 해당 상한을 초과 하는 경우는 <xref:System.IndexOutOfRangeException>예외 결과.</xref:System.IndexOutOfRangeException> 런타임 시 오류가 발생 컴파일러는 이러한 오류를 검색할 수 없습니다.  
  
### <a name="determining-bounds"></a>범위 결정  
 다른 구성 요소 코드를 배열에 전달 하는 경우 예를 들어 프로시저 인수로 알 수 없는 배열의 크기 또는 차원의 길이입니다. 항상 모든 요소에 액세스 하려고 하기 전에 모든 차원 배열에 대 한 상한을 결정 해야 합니다. 배열을 만든 수단으로 이외의 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] `New` 절 하한값 0 이외의 것 이므로 해당 한도를 결정 하는 것이 가장 안전 합니다.  
  
### <a name="specifying-the-dimension"></a>차원 지정  
 다차원 배열의 차수와 범위를 결정할 때는 주의 해야 치수를 지정 하는 방법입니다. `dimension` 의 매개 변수는 <xref:System.Array.GetLowerBound%2A>및 <xref:System.Array.GetUpperBound%2A>메서드는 0부터 시작 하는 동안는 `Rank` 의 매개 변수는 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] <xref:Microsoft.VisualBasic.Information.LBound%2A>및 <xref:Microsoft.VisualBasic.Information.UBound%2A>함수는 1부터 시작 합니다.</xref:Microsoft.VisualBasic.Information.UBound%2A> </xref:Microsoft.VisualBasic.Information.LBound%2A> </xref:System.Array.GetUpperBound%2A> </xref:System.Array.GetLowerBound%2A>  
  
## <a name="see-also"></a>참고 항목  
 [배열](../../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [방법: Visual Basic에서 배열 변수 초기화](../../../../visual-basic/programming-guide/language-features/arrays/how-to-initialize-an-array-variable.md)