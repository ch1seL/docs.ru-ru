---
title: 'Исключения: функция raise (F#)'
description: 'Узнайте, как используется функция F # «raise» указывает, что ошибку или исключительную ситуацию.'
ms.date: 05/16/2016
ms.openlocfilehash: 537d274659d29404380bfdd56310ac267372bb98
ms.sourcegitcommit: 3c1c3ba79895335ff3737934e39372555ca7d6d0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/05/2018
ms.locfileid: "43778263"
---
# <a name="exceptions-the-raise-function"></a>Исключения: функция raise

`raise` Функция используется для указания, что произошло ошибку или исключительную ситуацию. Сведения об ошибке записывается в объект исключения.

## <a name="syntax"></a>Синтаксис

```fsharp
raise (expression)
```

## <a name="remarks"></a>Примечания

`raise` Функция создает объект исключения и инициирует процесс освобождения стека. Процесс освобождения стека управляет среда CLR (CLR), поэтому этот процесс происходит так же, как в любом другом языке .NET. Процесс освобождения стека заключается в поиске обработчик исключений, который соответствует порожденное исключение. Поиск начинается в текущем `try...with` выражения, если таковой имеется. Каждый шаблон `with` блока установлен, в порядке. При обнаружении соответствующего обработчика исключений, исключение считается обработанным; в противном случае стек освобождается и `with` блоков в цепочке вызовов проверяются, пока не будет найден соответствующий обработчик. Любой `finally` блоки, которые встречаются в цепочке вызовов, также выполняются в последовательности раскрутки стека.

`raise` Функция является эквивалентом `throw` в C# или C++. Используйте `reraise` в обработчике catch для распространения вверх по цепи вызова одно и то же исключение.

В следующих примерах кода показано использование `raise` функция создает исключение.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet5801.fs)]

`raise` Функция также может использоваться для создания исключений .NET, как показано в следующем примере.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet5802.fs)]

## <a name="see-also"></a>См. также

- [Обработка исключений](index.md)
- [Типы исключения](exception-types.md)
- [Исключения: выражение `try...with`](the-try-with-expression.md)
- [Исключения: выражение `try...finally`](the-try-finally-expression.md)
- [Исключения: функция `failwith`](the-failwith-function.md)
- [Исключения: функция `invalidArg`](the-invalidArg-function.md)
