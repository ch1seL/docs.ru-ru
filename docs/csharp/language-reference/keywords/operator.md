---
title: Ключевое слово operator (справочник по C#)
description: Сведения о том, как перегрузить встроенные операторы C#
ms.date: 08/27/2018
f1_keywords:
- operator_CSharpKeyword
- operator
helpviewer_keywords:
- operator keyword [C#]
ms.assetid: 59218cce-e90e-42f6-a6bb-30300981b86a
ms.openlocfilehash: 1e11d7767b61becc39b1158fae9cb2abe997e4bd
ms.sourcegitcommit: ad99773e5e45068ce03b99518008397e1299e0d1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/22/2018
ms.locfileid: "46525754"
---
# <a name="operator-c-reference"></a>operator (Справочник по C#)

Ключевое слово `operator` используется для перегрузки встроенного оператора или выполнения пользовательского преобразования в объявлении класса или структуры.

Чтобы перегрузить оператор в пользовательском классе или структуре, создайте объявление оператора в соответствующем типе. Объявление оператора, которое перегружает встроенный оператор C#, должно удовлетворять следующим правилам:

- Оно должно включать `public` и модификатор `static`.
- Оно должно включать `operator X`, где `X` — имя или обозначение перегружаемого оператора.
- Унарные операторы имеют один параметр, а бинарные операторы имеют два параметра. В каждом случае по крайней мере один параметр должен иметь тот же тип, что и класс или структура, в которых объявлен этот оператор.

Сведения о том, как определить операторы преобразования, см. в разделах, посвященных ключевым словам [explicit](explicit.md) и [implicit](implicit.md).

Обзор операторов C#, которые могут быть перегружены, см. в разделе [Перегружаемые операторы](../../programming-guide/statements-expressions-operators/overloadable-operators.md).

## <a name="example"></a>Пример

В следующем примере определяется тип `Fraction`, представляющий дробные числа. Он перегружает операторы `+` и `*` для выполнения сложения и умножения, а также предоставляет оператор преобразования, который преобразует тип `Fraction` в тип `double`.

[!code-csharp[csrefKeywordsConversion#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsConversion/CS/csrefKeywordsConversion.cs#6)]

## <a name="c-language-specification"></a>Спецификация языка C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>См. также

- [Справочник по C#](../index.md)
- [Руководство по программированию на C#](../../programming-guide/index.md)
- [Ключевые слова в C#](index.md)
- [implicit](implicit.md)
- [explicit](explicit.md)
- [Перегружаемые операторы](../../programming-guide/statements-expressions-operators/overloadable-operators.md)
- [Практическое руководство. Реализация определенных пользователем преобразований между структурами](../../programming-guide/statements-expressions-operators/how-to-implement-user-defined-conversions-between-structs.md)
