---
title: Новые возможности C# — руководство по C#
description: Как развивается язык C#
ms.date: 11/13/2017
ms.assetid: 77deec51-a14d-46d4-9bb3-faf449477149
ms.openlocfilehash: 399550178a12ff520dff033f0f1dc4a7cdfb9591
ms.sourcegitcommit: c217b067985905cb21eafc5dd9a83568d7ff4e45
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/22/2018
ms.locfileid: "36314676"
---
# <a name="whats-new-in-c"></a>Новые возможности C# #

Эта страница содержит план новых возможностей в каждой основной версии языка C#. Перейдя по ссылкам ниже, вы сможете получить подробные сведения по основным возможностям, добавленным в каждом выпуске.

> [!IMPORTANT]
> В некоторых возможностях используются типы и методы в *стандартной библиотеке* языка C#, например, обработка исключений. Каждая инструкция и выражение `throw` проверяется, чтобы убедиться, что вызываемый объект является производным от <xref:System.Exception>. Аналогичным образом каждая инструкция `catch` проверяется, чтобы убедиться, что перехваченный тип является производным от <xref:System.Exception>. В каждой версии могут добавляться новые требования. Чтобы использовать новейшие возможности языка в старой среде, может потребоваться установить определенные библиотеки. Эти зависимости описаны на странице для каждой конкретной версии. Дополнительные сведения о связи между языком и библиотекой, а также общие сведения о такой зависимости см. [здесь](relationships-between-language-and-library.md). 

Чтобы использовать новые возможности доработанного выпуска, [настройте версию языка компилятора](../language-reference/configure-language-version.md), выбрав необходимую.

* [C# 7.3](csharp-7-3.md).
  - На этой странице описываются новейшие функции в языке C#. Версия C# 7.3 сейчас доступна в [Visual Studio 2017 версии 15.7](https://visualstudio.microsoft.com/vs/whatsnew/) и в [пакете SDK для .NET Core 2.1 (2.1.300 RC1)](../../core/whats-new/index.md).
* [C# 7.2](csharp-7-2.md).
  - На этой странице описаны функции, добавленные в язык C#. C# 7.2 сейчас доступен в [Visual Studio 2017 версии 15.5](https://visualstudio.microsoft.com/vs/whatsnew/) и в [пакете SDK для .NET Core 2.0](../../core/whats-new/index.md).
* [C# 7.1](csharp-7-1.md).
  - На этой странице описаны функции, добавленные в C# 7.1. Эти функции были добавлены в [Visual Studio 2017 версии 15.3](https://visualstudio.microsoft.com/vs/whatsnew/) и в [пакет SDK для .NET Core 2.0](../../core/whats-new/index.md).
* [C# 7.0](csharp-7.md).
  - На этой странице описываются функции, добавленные в C# 7.0. Они были добавлены в [Visual Studio 2017](https://visualstudio.microsoft.com/vs/whatsnew/), [.NET Core 1.0](../../core/whats-new/index.md) и более поздние версии.
* [C# 6](csharp-6.md)
  - На этой странице описываются функции, добавленные в C# 6. Эти функции доступны в Visual Studio 2015 для разработчиков Windows и в .NET Core 1.0 для разработчиков, исследующих C# на macOS и Linux.
* [Кроссплатформенная поддержка](../../core/index.md)
  - Благодаря поддержке .NET Core язык C# работает на многих платформах. Если вы хотите попробовать C# на macOS или на одном из множества поддерживаемых дистрибутивов Linux, узнайте больше о .NET Core.
* [Пакет SDK для платформы компилятора .NET](../roslyn-sdk/index.md).
  - Пакет SDK для платформы компилятора .NET позволяет создавать код на языке C#, который выполняет статический анализ. Вы можете использовать эти API, чтобы найти возможные ошибки, нерекомендуемые параметры или предлагать исправления и реализовать их.

## <a name="previous-versions"></a>Предыдущие версии

Ниже перечислены основные функции, представленные в предыдущих версиях языка C# и Visual Studio .NET.

* Visual Studio .NET 2013
  - Эта версия Visual Studio включала исправления ошибок, улучшения производительности и предварительные версии технологий .NET Compiler Platform (Roslyn), которые теперь входят в [пакет SDK для .NET Compiler Platform](../roslyn-sdk/index.md).
* C# 5, Visual Studio .NET 2012
  - `Async` / `await`, и атрибуты [сведений о вызывающем объекте](../programming-guide/concepts/caller-information.md).
* C# 4, Visual Studio .NET 2010
  - `Dynamic`, [именованные аргументы](../programming-guide/classes-and-structs/named-and-optional-arguments.md), дополнительные параметры и [ковариации и контрвариантность](../programming-guide/concepts/covariance-contravariance/index.md) в универсальных шаблонах.
* C# 3, Visual Studio .NET 2008
  - Инициализаторы объектов и коллекций, лямбда-выражения, методы расширений, анонимные типы, автоматические свойства, вывод локального типа `var` и [LINQ](../programming-guide/concepts/linq/index.md).
* C# 2, Visual Studio .NET 2005
  - Анонимные методы, универсальные шаблоны, типы, допускающие значение NULL, итераторы и приостановки, классы `static`, ковариации и контрвариантность для делегатов.
* C# 1.1, Visual Studio .NET 2003
  - `#line` pragma и комментарии XML-документации.
* C# 1, Visual Studio .NET 2002
  - Первый выпуск [C#](../csharp.md).
