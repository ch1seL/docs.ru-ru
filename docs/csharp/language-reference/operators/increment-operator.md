---
title: Оператор ++ (справочник по C#)
ms.date: 07/20/2015
f1_keywords:
- ++_CSharpKeyword
helpviewer_keywords:
- increment operator (++) [C#]
- ++ operator [C#]
ms.assetid: e9dec353-070b-44fb-98ed-eb8fdf753feb
ms.openlocfilehash: a52f614ce1bbfb8e9d9be686b277c1e69f6f9d35
ms.sourcegitcommit: ad99773e5e45068ce03b99518008397e1299e0d1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/22/2018
ms.locfileid: "46580074"
---
# <a name="-operator-c-reference"></a>Оператор ++ (справочник по C#)
Оператор инкремента (`++`) увеличивает операнд на 1. Оператор инкремента может находиться перед своим операндом или после него: `++variable` и `variable++`.  
  
## <a name="remarks"></a>Примечания  
 Первый случай — это операция префиксного инкремента. Результатом операции является значение операнда после его увеличения.  
  
 Второй случай — это операция постфиксного инкремента. Результатом операции является значение операнда до его увеличения.  
  
 Числовые типы и типы перечислений имеют предварительно определенные операторы инкремента. Определяемые пользователем типы могут перегружать оператор `++` . Операции с целыми типами обычно разрешены и для перечислений.  
  
## <a name="example"></a>Пример  
 [!code-csharp[csRefOperators#3](../../../csharp/language-reference/operators/codesnippet/CSharp/increment-operator_1.cs)]  
  
## <a name="see-also"></a>См. также

- [Справочник по C#](../../../csharp/language-reference/index.md)  
- [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)  
- [Операторы в C#](../../../csharp/language-reference/operators/index.md)
