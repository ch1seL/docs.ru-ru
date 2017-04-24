---
title: "Разрешение перегрузки (Visual Basic) | Документы Microsoft"
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
- Visual Basic code, procedures
- overload resolution
- procedures, overloading
- procedures, calling
- procedure overloading, overload resolution
- signatures, procedure
- overloads, resolution
ms.assetid: 766115d1-4352-45fb-859f-6063e0de0ec0
caps.latest.revision: 21
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: 0de3a603fa84a72018a566f6e7182b45e53ec89e
ms.lasthandoff: 03/13/2017

---
# <a name="overload-resolution-visual-basic"></a>Разрешение перегрузки (Visual Basic)
Когда [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] компилятор обнаруживает вызов процедуры, которая определена в несколько перегруженных версий, компилятор должен определить, какую перегрузку необходимо вызвать. Это делается путем выполнения следующих шагов:  
  
1.  **Специальные возможности.** Это исключает все перегрузки с уровнем доступа, вызов этого метода не позволяет вызывающему коду.  
  
2.  **Число параметров.** Это исключает любые перегрузку, которая определяет разное число параметров, чем задано в вызове.  
  
3.  **Типы данных параметров.** Компилятор предпочтительнее использует методы экземпляра по сравнению с методами расширения. Если найден метод экземпляра, требующий только расширяющие преобразования для сопоставления вызову процедуры, удаляются все методы расширения, и компилятор продолжает использовать только кандидаты метода экземпляра. Если такой метод экземпляр не найден, он продолжает выполнение экземпляра и методы расширения.  
  
     На этом шаге рассмотрения исключаются те перегруженные версии, для которых типы данных аргументов вызова не может быть преобразованы в типы параметров, определенные в этой перегрузке.  
  
4.  **Сужающие преобразования.** Это исключает любые перегрузка, которая требует сужающее преобразование типов аргументов вызова в определенные типы параметров. Это верно ли переключатель проверки типов ([оператор Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md)) является `On` или `Off`.  
  
5.  **Наименьшее расширение.** Компилятор рассматривают оставшиеся перегрузки парами. Для каждой пары компилятор сравнивает типы данных определенных параметров. Если в одной из перегрузок все типы расширяются до соответствующих типов в другой, компилятор исключает последнюю. То есть остается перегрузка, которая требует меньшего расширения при преобразовании.  
  
6.  **Единственный вариант.** Компилятор продолжает рассматривать перегрузки попарно до только одна перегрузка остается, и он разрешает вызов этой перегрузки. Если компилятор не может снизить перегрузки единственный вариант, он создает ошибку.  
  
 Ниже показан процесс, который определяет набор перегруженных версий для вызова.  
  
 ![Схема потока перегруженного процесса разрешения](./media/overloadres.gif "OverloadRes")  
Разрешение для перегруженных версий  
  
 Следующий пример иллюстрирует этот процесс разрешения перегрузки.  
  
 [!code-vb[VbVbcnProcedures&#62;](./codesnippet/VisualBasic/overload-resolution_1.vb)]  
  
 [!code-vb[VbVbcnProcedures&#63;](./codesnippet/VisualBasic/overload-resolution_2.vb)]  
  
 В первом вызове компилятор устраняет первую перегрузку, так как тип первого аргумента (`Short`) сужается к типу соответствующего параметра (`Byte`). Затем исключаются третья перегрузка, так как каждый тип аргумента во второй перегрузке (`Short` и `Single`) может быть расширен до соответствующего типа в третьей перегрузке (`Integer` и `Single`). Вторая перегрузка требует меньшего расширения, поэтому компилятор использует ее для вызова.  
  
 Во втором вызове компилятор не может устранить любую из перегрузок зависимости от сужения. Он исключаются третья перегрузка по тем же причинам, как в первом вызове, поскольку можно вызвать вторую перегрузку с меньшим расширением типов аргументов. Однако компилятор не может разрешить между первой и второй перегрузок. Каждая имеет один определенный тип параметра, может быть расширен до соответствующего типа в другой (`Byte` для `Short`, но `Single` для `Double`). Поэтому компилятор создает ошибку разрешения перегрузки.  
  
## <a name="overloaded-optional-and-paramarray-arguments"></a>Перегрузка необязательных аргументов и массива аргументов  
 Если две перегрузки процедуры имеют идентичные подписи, за исключением того, что последний параметр объявляется [необязательно](../../../../visual-basic/language-reference/modifiers/optional.md) в одном и [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) в другой, компилятор разрешает вызов процедуры, следующим образом:  
  
|Если задан как последний аргумент при вызове|Компилятор вызывает перегрузку, объявление как последний аргумент|  
|---|---|  
|Нет значения (аргумент опущен)|`Optional`|  
|Одиночное значение|`Optional`|  
|Два или более значений в список разделенных запятыми|`ParamArray`|  
|Массив произвольной длины (включая пустой массив)|`ParamArray`|  
  
## <a name="see-also"></a>См. также  
 [Необязательные параметры](./optional-parameters.md)   
 [Массивы параметров](./parameter-arrays.md)   
 [Перегрузка процедур](./procedure-overloading.md)   
 [Рекомендации по устранению неполадок](./troubleshooting-procedures.md)   
 [Практическое руководство: определение различных версий процедуры](./how-to-define-multiple-versions-of-a-procedure.md)   
 [Практическое руководство: вызов перегруженной процедуры](./how-to-call-an-overloaded-procedure.md)   
 [Практическое руководство: перегрузка процедуры, которая принимает необязательные параметры](./how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [Практическое руководство: перегрузка процедуры, принимающей неопределенное число параметров](./how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)   
 [Вопросы, связанные с перегрузкой процедур](./considerations-in-overloading-procedures.md)   
 [Перегруженные методы](../../../../visual-basic/language-reference/modifiers/overloads.md)   
 [Методы расширения](./extension-methods.md)