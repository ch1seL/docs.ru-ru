---
title: "Команда dotnet-run | Microsoft Docs"
description: "Команда dotnet-run — это удобное средство для запуска приложения из исходного кода."
keywords: "dotnet-run, CLI, команда CLI, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 10/07/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 40d4e60f-9900-4a48-b03c-0bae06792d91
translationtype: Human Translation
ms.sourcegitcommit: 2ad428dcda9ef213a8487c35a48b33929259abba
ms.openlocfilehash: 066fbcd9f342233fb12599a84211675ba5b95860

---

#<a name="dotnet-run-tooling-preview-4"></a>dotnet-run (предварительная версия 4 инструментов)

> [!WARNING]
> Эта статья применима к инструментам .NET Core (предварительная версия 4) для версии-кандидата Visual Studio 2017. Версия этой статьи об инструментах .NET Core (предварительная версия 2): [dotnet-run](../../tools/dotnet-run.md).

## <a name="name"></a>Имя 

dotnet-run — выполняет исходный код "на месте" без дополнительных явных команд компиляции или запуска.

## <a name="synopsis"></a>Краткий обзор

`dotnet run [--help] [--framework] [--configuration]
    [--project] [[--] [application arguments]]`

## <a name="description"></a>Описание
`dotnet run` — это удобное средство для запуска приложения из исходного кода одной командой. Команда компилирует исходный код, создает выходную программу, а затем запускает ее. Она полезна для быстрой итеративной разработки, а также может использоваться для запуска программ с распределенным исходным кодом (например, веб-сайта).

Эта команда использует [dotnet build](dotnet-build.md) для создания сборки .NET на основе входного исходного кода перед запуском программы. Требования этой команды и способ обработки входного исходного кода наследуются от команды сборки. Дополнительные сведения об этих требованиях содержатся в документации по команде сборки.

Выходные файлы записываются в дочернюю папку *bin*, которая будет создана, если она еще не существует. При необходимости файлы будут перезаписаны. Временные файлы записываются в дочернюю папку *obj*.  

Если в проекте указано несколько платформ, `dotnet run` сначала выбирает платформы .NET Core. Если их нет, возникает ошибка. Чтобы указать другие платформы, используйте аргумент `--framework`.

Команда `dotnet run` должна использоваться в контексте проектов, а не созданных сборок. Если вместо этого вы пытаетесь запустить библиотеку DLL переносимого приложения, следует использовать [dotnet](dotnet.md) без какой-либо команды, как в следующем примере.
 
`dotnet myapp.dll`

Дополнительные сведения о драйвере `dotnet` см. в разделе [Средства интерфейса командной строки (CLI) .NET Core](index.md).

## <a name="options"></a>Параметры

`--`

Отделяет аргументы, предназначенные для `dotnet run`, от аргументов для выполняемого приложения. Все аргументы после этого будут переданы выполняемому приложению. 

`-h|--help`

Выводит краткую справку по команде.

`-f`, `--framework <FRAMEWORK_IDENTIFIER>`

Выполняет приложение для указанного идентификатора платформы (FID). 

`-c`, `--configuration <Debug|Release>`

Конфигурация, используемая при публикации. Значение по умолчанию — `Debug`.

`-p`, `--project [PATH]`

Указывает выполняемый проект. Это может быть путь к файлу [csproj](csproj.md) или каталогу, который содержит файл [csproj](csproj.md). Если значение не задано, по умолчанию используется текущий каталог. 

## <a name="examples"></a>Примеры

Выполнение проекта в текущем каталоге: `dotnet run` 

Выполнение указанного проекта:

`dotnet run --project /projects/proj1/proj1.csproj`

Выполнение проекта в текущем каталоге (аргумент `--help` в этом примере передается выполняемому приложению, так как используется аргумент `--`):

`dotnet run --configuration Release -- --help`


<!--HONumber=Jan17_HO3-->

