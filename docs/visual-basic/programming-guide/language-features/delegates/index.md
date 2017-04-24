---
title: "Делегаты (Visual Basic) | Документация Майкрософт"
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
- delegates [Visual Basic]
- Visual Basic code, delegates
ms.assetid: 410b60dc-5e60-4ec0-bfae-426755a2ee28
caps.latest.revision: 10
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 0fad74980e3c8cf66b9909b50bdaa3f9f4f567a1
ms.lasthandoff: 03/13/2017

---
# <a name="delegates-visual-basic"></a>Делегаты (Visual Basic)
Делегаты являются объектами, которые ссылаются на методы. Иногда их описывают как *типобезопасные указатели функций*, поскольку они похожи на указатели функций, используемые в других языках программирования. Но в отличии от указателей функций, делегаты [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] являются ссылочными типами и основаны на классе <xref:System.Delegate?displayProperty=fullName>. Делегаты могут ссылаться на оба вида общих методов — на методы, которые могут вызываться без определенного экземпляра класса, и на методы экземпляра.  
  
## <a name="delegates-and-events"></a>Делегаты и события  
 Делегаты полезны в тех ситуациях, когда требуется промежуточное звено между вызывающей и вызываемой процедурами. Например, вы хотите создать объект, который создает события и в зависимости от обстоятельств может вызывать разные обработчики событий. К сожалению, этот объект не может знать заранее, какой обработчик событий обрабатывает конкретное событие. В [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] вы можете динамически связывать обработчики событий с событиями. Для этого при вызове инструкции `AddHandler` создается делегат. Во время выполнения делегат передает вызовы в соответствующий обработчик событий.  
  
 У вас есть возможность создавать свои собственные делегаты, но в большинстве случаев [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] самостоятельно создает делегат и выполняет все необходимые действия. Например, инструкция `Event` неявно определяет класс делегата с именем `<EventName>EventHandler`. Он размещается как вложенный класс в том классе, который содержит инструкцию `Event`, а его сигнатура совпадает с сигнатурой события. Инструкция `AddressOf` неявно создает экземпляр делегата, который ссылается на конкретную процедуру. Следующие два фрагмента кода эквивалентны. В первой строке вы видите явное создание экземпляра `Eventhandler`, который ссылается на метод `Button1_Click`, переданный в качестве аргумента. Вторая строка делает то же самое, но более удобна в использовании.  
  
 [!code-vb[VbVbalrDelegates#6](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/delegates_1.vb)]  
  
 Сокращенный способ создания делегатов вы можете использовать в любом месте кода, где компилятор может определить тип делегата по контексту.  
  
## <a name="declaring-events-that-use-an-existing-delegate-type"></a>Объявление событий, использующих существующий тип делегата  
 В некоторых ситуациях вам потребуется объявить, чтобы событие использовало в качестве своего делегата уже существующий тип делегата. Для этого используется следующий синтаксис:  
  
 [!code-vb[VbVbalrDelegates#7](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/delegates_2.vb)]  
  
 Это удобно, когда нужно направить к одному обработчику несколько событий.  
  
## <a name="delegate-variables-and-parameters"></a>Переменные и параметры делегата  
 Делегаты можно использовать для других, не связанных с событиями задач, например в свободной потоковой модели или в процедурах, которые должны вызывать разные версии функции во время выполнения.  
  
 Предположим, у вас есть рекламное приложения, которое содержит список с названиями автомобилей. Рекламные объявления сортируются по названию, которое обычно содержит модель автомобиля. Если у некоторых автомобилей перед моделью указан год производства, возникает проблема. Эта проблема связана с тем, что встроенная функция сортировки упорядочивает значения только по кодам знаков. В результате все объявления, которые начинаются с даты, располагаются первыми, и лишь затем идут объявления с моделью в начале строки.  
  
 Чтобы устранить эту проблему, можно создать в классе специальную процедуру сортировки, которая для большинства списков использует стандартную сортировку по алфавиту, но во время выполнения переключается на пользовательскую сортировку для объявлений о продаже автомобилей. Для этого во время выполнения пользовательская процедура сортировки передается классу сортировки с помощью делегатов.  
  
## <a name="addressof-and-lambda-expressions"></a>AddressOf и лямбда-выражения  
 Каждый класс делегата определяет конструктор, которому передается спецификация метода объекта. Аргумент конструктора делегата должен быть ссылкой на метод или лямбда-выражение.  
  
 Чтобы указать ссылку на метод, используйте следующий синтаксис:  
  
 `AddressOf` [`expression`.]`methodName`  
  
 Тип `expression` во время компиляции должен представлять собой имя класса или интерфейса, который содержит метод с указанным именем, сигнатура которого соответствует сигнатуре класса делегата. `methodName` должен быть общим методом или методом экземпляра. `methodName` всегда является обязательным, даже если делегат создается для метода по умолчанию в классе.  
  
 Чтобы указать лямбда-выражение, используйте следующий синтаксис:  
  
 `Function` ([`parm` As `type`, `parm2` As `type2`, ...]) `expression`  
  
 В следующем примере показано, как использовать `AddressOf` и лямбда-выражения для указания ссылки на делегат.  
  
 [!code-vb[VbVbalrDelegates#15](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/delegates_3.vb)]  
  
 Сигнатура функции должна соответствовать сигнатуре типа делегата. Дополнительные сведения о лямбда-выражениях см. в разделе [Лямбда-выражения](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md). Дополнительные примеры лямбда-выражений и назначений `AddressOf` делегатам см. в статье [Relaxed Delegate Conversion](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md) (Неявное преобразование делегата).  
  
## <a name="related-topics"></a>Связанные разделы  
  
|Заголовок|Описание|  
|-----------|-----------------|  
|[Практическое руководство. Вызов метода делегата](../../../../visual-basic/programming-guide/language-features/delegates/how-to-invoke-a-delegate-method.md)|Предоставляет пример, в котором показано, как связать метод с делегатом и вызвать этот метод через делегат.|  
|[How to: Pass Procedures to Another Procedure in Visual Basic](../../../../visual-basic/programming-guide/language-features/delegates/how-to-pass-procedures-to-another-procedure.md) (Практическое руководство. Передача процедур другой процедуре в Visual Basic)|Демонстрирует использование делегатов для передачи одной процедуры в другую процедуру.|  
|[Неявное преобразование делегата](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)|Описывает, как можно назначить делегаты или обработчики для подпрограмм и функций, если их сигнатуры не совпадают|  
|[События](../../../../visual-basic/programming-guide/language-features/events/index.md)|Предоставляет обзор событий в Visual Basic.|