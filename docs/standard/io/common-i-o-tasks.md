---
title: "Общие задачи с вводом выводом"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: I/O, common tasks
ms.assetid: bf00c380-706a-4e38-b829-454a480629fc
caps.latest.revision: "15"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 51238020f4d93ad32dac85a95d7b1cab26f2dd64
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="common-io-tasks"></a><span data-ttu-id="aa77a-102">Распространенные задачи ввода-вывода</span><span class="sxs-lookup"><span data-stu-id="aa77a-102">Common I/O Tasks</span></span>
<span data-ttu-id="aa77a-103">Пространство имен <xref:System.IO> предоставляет несколько классов, которые позволяют выполнять с файлами, каталогами и потоками различные действия, такие как чтение и запись.</span><span class="sxs-lookup"><span data-stu-id="aa77a-103">The <xref:System.IO> namespace provides several classes that allow for various actions, such as reading and writing, to be performed on files, directories, and streams.</span></span> <span data-ttu-id="aa77a-104">Дополнительные сведения см. в разделе [файловый и потоковый с вводом выводом](../../../docs/standard/io/index.md).</span><span class="sxs-lookup"><span data-stu-id="aa77a-104">For more information, see [File and Stream I-O](../../../docs/standard/io/index.md).</span></span>  
  
## <a name="common-file-tasks"></a><span data-ttu-id="aa77a-105">Распространенные задачи с файлами</span><span class="sxs-lookup"><span data-stu-id="aa77a-105">Common File Tasks</span></span>  
  
|<span data-ttu-id="aa77a-106">Действие</span><span class="sxs-lookup"><span data-stu-id="aa77a-106">To do this...</span></span>|<span data-ttu-id="aa77a-107">Раздел с примером</span><span class="sxs-lookup"><span data-stu-id="aa77a-107">See the example in this topic...</span></span>|  
|-------------------|--------------------------------------|  
|<span data-ttu-id="aa77a-108">Создание текстового файла</span><span class="sxs-lookup"><span data-stu-id="aa77a-108">Create a text file</span></span>|<span data-ttu-id="aa77a-109">Метод <xref:System.IO.File.CreateText%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-109"><xref:System.IO.File.CreateText%2A?displayProperty=nameWithType> method</span></span><br /><br /> <span data-ttu-id="aa77a-110">Метод <xref:System.IO.FileInfo.CreateText%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-110"><xref:System.IO.FileInfo.CreateText%2A?displayProperty=nameWithType> method</span></span><br /><br /> <span data-ttu-id="aa77a-111">Метод <xref:System.IO.File.Create%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-111"><xref:System.IO.File.Create%2A?displayProperty=nameWithType> method</span></span><br /><br /> <span data-ttu-id="aa77a-112">Метод <xref:System.IO.FileInfo.Create%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-112"><xref:System.IO.FileInfo.Create%2A?displayProperty=nameWithType> method</span></span>|  
|<span data-ttu-id="aa77a-113">Запись в текстовый файл</span><span class="sxs-lookup"><span data-stu-id="aa77a-113">Write to a text file</span></span>|[<span data-ttu-id="aa77a-114">Практическое руководство. Запись текста в файл</span><span class="sxs-lookup"><span data-stu-id="aa77a-114">How to: Write Text to a File</span></span>](../../../docs/standard/io/how-to-write-text-to-a-file.md)<br /><br /> [<span data-ttu-id="aa77a-115">Практическое руководство. Запись данных в текстовый файл (C++/CLI)</span><span class="sxs-lookup"><span data-stu-id="aa77a-115">How to: Write a Text File (C++/CLI)</span></span>](/cpp/dotnet/how-to-write-a-text-file-cpp-cli)|  
|<span data-ttu-id="aa77a-116">Чтение из текстового файла</span><span class="sxs-lookup"><span data-stu-id="aa77a-116">Read from a text file</span></span>|[<span data-ttu-id="aa77a-117">Практическое руководство. Считывание текста из файла</span><span class="sxs-lookup"><span data-stu-id="aa77a-117">How to: Read Text from a File</span></span>](../../../docs/standard/io/how-to-read-text-from-a-file.md)|  
|<span data-ttu-id="aa77a-118">Добавление текста в файл</span><span class="sxs-lookup"><span data-stu-id="aa77a-118">Append text to a file</span></span>|[<span data-ttu-id="aa77a-119">Практическое руководство. Открытие файла журнала и добавление в него данных</span><span class="sxs-lookup"><span data-stu-id="aa77a-119">How to: Open and Append to a Log File</span></span>](../../../docs/standard/io/how-to-open-and-append-to-a-log-file.md)<br /><br /> <span data-ttu-id="aa77a-120">Метод <xref:System.IO.File.AppendText%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-120"><xref:System.IO.File.AppendText%2A?displayProperty=nameWithType> method</span></span><br /><br /> <span data-ttu-id="aa77a-121">Метод <xref:System.IO.FileInfo.AppendText%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-121"><xref:System.IO.FileInfo.AppendText%2A?displayProperty=nameWithType> method</span></span>|  
|<span data-ttu-id="aa77a-122">Переименование или перемещение файла</span><span class="sxs-lookup"><span data-stu-id="aa77a-122">Rename or move a file</span></span>|<span data-ttu-id="aa77a-123">Метод <xref:System.IO.File.Move%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-123"><xref:System.IO.File.Move%2A?displayProperty=nameWithType> method</span></span><br /><br /> <span data-ttu-id="aa77a-124">Метод <xref:System.IO.FileInfo.MoveTo%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-124"><xref:System.IO.FileInfo.MoveTo%2A?displayProperty=nameWithType> method</span></span>|  
|<span data-ttu-id="aa77a-125">Удаление файла</span><span class="sxs-lookup"><span data-stu-id="aa77a-125">Delete a file</span></span>|<span data-ttu-id="aa77a-126">Метод <xref:System.IO.File.Delete%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-126"><xref:System.IO.File.Delete%2A?displayProperty=nameWithType> method</span></span><br /><br /> <span data-ttu-id="aa77a-127">Метод <xref:System.IO.FileInfo.Delete%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-127"><xref:System.IO.FileInfo.Delete%2A?displayProperty=nameWithType> method</span></span>|  
|<span data-ttu-id="aa77a-128">Копирование файла</span><span class="sxs-lookup"><span data-stu-id="aa77a-128">Copy a file</span></span>|<span data-ttu-id="aa77a-129">Метод <xref:System.IO.File.Copy%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-129"><xref:System.IO.File.Copy%2A?displayProperty=nameWithType> method</span></span><br /><br /> <span data-ttu-id="aa77a-130">Метод <xref:System.IO.FileInfo.CopyTo%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-130"><xref:System.IO.FileInfo.CopyTo%2A?displayProperty=nameWithType> method</span></span>|  
|<span data-ttu-id="aa77a-131">Получение сведений о размере файла</span><span class="sxs-lookup"><span data-stu-id="aa77a-131">Get the size of a file</span></span>|<span data-ttu-id="aa77a-132">Свойство <xref:System.IO.FileInfo.Length%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-132"><xref:System.IO.FileInfo.Length%2A?displayProperty=nameWithType> property</span></span>|  
|<span data-ttu-id="aa77a-133">Получение атрибутов файла</span><span class="sxs-lookup"><span data-stu-id="aa77a-133">Get the attributes of a file</span></span>|<span data-ttu-id="aa77a-134">Метод <xref:System.IO.File.GetAttributes%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-134"><xref:System.IO.File.GetAttributes%2A?displayProperty=nameWithType> method</span></span>|  
|<span data-ttu-id="aa77a-135">Установка атрибутов файла</span><span class="sxs-lookup"><span data-stu-id="aa77a-135">Set the attributes of a file</span></span>|<span data-ttu-id="aa77a-136">Метод <xref:System.IO.File.SetAttributes%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-136"><xref:System.IO.File.SetAttributes%2A?displayProperty=nameWithType> method</span></span>|  
|<span data-ttu-id="aa77a-137">Определение существования файла</span><span class="sxs-lookup"><span data-stu-id="aa77a-137">Determine whether a file exists</span></span>|<span data-ttu-id="aa77a-138">Метод <xref:System.IO.File.Exists%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-138"><xref:System.IO.File.Exists%2A?displayProperty=nameWithType> method</span></span>|  
|<span data-ttu-id="aa77a-139">Чтение из двоичного файла</span><span class="sxs-lookup"><span data-stu-id="aa77a-139">Read from a binary file</span></span>|[<span data-ttu-id="aa77a-140">Практическое руководство. Считывание из нового файла данных и запись в этот файл</span><span class="sxs-lookup"><span data-stu-id="aa77a-140">How to: Read and Write to a Newly Created Data File</span></span>](../../../docs/standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)|  
|<span data-ttu-id="aa77a-141">Запись в двоичный файл</span><span class="sxs-lookup"><span data-stu-id="aa77a-141">Write to a binary file</span></span>|[<span data-ttu-id="aa77a-142">Практическое руководство. Считывание из нового файла данных и запись в этот файл</span><span class="sxs-lookup"><span data-stu-id="aa77a-142">How to: Read and Write to a Newly Created Data File</span></span>](../../../docs/standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)|  
|<span data-ttu-id="aa77a-143">Извлечение расширения имени файла</span><span class="sxs-lookup"><span data-stu-id="aa77a-143">Retrieve a file name extension</span></span>|<span data-ttu-id="aa77a-144">Метод <xref:System.IO.Path.GetExtension%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-144"><xref:System.IO.Path.GetExtension%2A?displayProperty=nameWithType> method</span></span>|  
|<span data-ttu-id="aa77a-145">Извлечение полного пути к файлу</span><span class="sxs-lookup"><span data-stu-id="aa77a-145">Retrieve the fully qualified path of a file</span></span>|<span data-ttu-id="aa77a-146">Метод <xref:System.IO.Path.GetFullPath%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-146"><xref:System.IO.Path.GetFullPath%2A?displayProperty=nameWithType> method</span></span>|  
|<span data-ttu-id="aa77a-147">Извлечение имени и расширения файла из пути</span><span class="sxs-lookup"><span data-stu-id="aa77a-147">Retrieve the file name and extension from a path</span></span>|<span data-ttu-id="aa77a-148">Метод <xref:System.IO.Path.GetFileName%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-148"><xref:System.IO.Path.GetFileName%2A?displayProperty=nameWithType> method</span></span>|  
|<span data-ttu-id="aa77a-149">Изменение расширения файла</span><span class="sxs-lookup"><span data-stu-id="aa77a-149">Change the extension of a file</span></span>|<span data-ttu-id="aa77a-150">Метод <xref:System.IO.Path.ChangeExtension%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-150"><xref:System.IO.Path.ChangeExtension%2A?displayProperty=nameWithType> method</span></span>|  
  
## <a name="common-directory-tasks"></a><span data-ttu-id="aa77a-151">Распространенные задачи с каталогами</span><span class="sxs-lookup"><span data-stu-id="aa77a-151">Common Directory Tasks</span></span>  
  
|<span data-ttu-id="aa77a-152">Действие</span><span class="sxs-lookup"><span data-stu-id="aa77a-152">To do this...</span></span>|<span data-ttu-id="aa77a-153">Раздел с примером</span><span class="sxs-lookup"><span data-stu-id="aa77a-153">See the example in this topic...</span></span>|  
|-------------------|--------------------------------------|  
|<span data-ttu-id="aa77a-154">Доступ к файлу в особой папке, например "Мои документы"</span><span class="sxs-lookup"><span data-stu-id="aa77a-154">Access a file in a special folder such as My Documents</span></span>|[<span data-ttu-id="aa77a-155">Практическое руководство. Запись текста в файл</span><span class="sxs-lookup"><span data-stu-id="aa77a-155">How to: Write Text to a File</span></span>](../../../docs/standard/io/how-to-write-text-to-a-file.md)|  
|<span data-ttu-id="aa77a-156">Создание каталога</span><span class="sxs-lookup"><span data-stu-id="aa77a-156">Create a directory</span></span>|<span data-ttu-id="aa77a-157">Метод <xref:System.IO.Directory.CreateDirectory%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-157"><xref:System.IO.Directory.CreateDirectory%2A?displayProperty=nameWithType> method</span></span><br /><br /> <span data-ttu-id="aa77a-158">Свойство <xref:System.IO.FileInfo.Directory%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-158"><xref:System.IO.FileInfo.Directory%2A?displayProperty=nameWithType> property</span></span>|  
|<span data-ttu-id="aa77a-159">Создание подкаталога</span><span class="sxs-lookup"><span data-stu-id="aa77a-159">Create a subdirectory</span></span>|<span data-ttu-id="aa77a-160">Метод <xref:System.IO.DirectoryInfo.CreateSubdirectory%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-160"><xref:System.IO.DirectoryInfo.CreateSubdirectory%2A?displayProperty=nameWithType> method</span></span>|  
|<span data-ttu-id="aa77a-161">Переименование или перемещение каталога</span><span class="sxs-lookup"><span data-stu-id="aa77a-161">Rename or move a directory</span></span>|<span data-ttu-id="aa77a-162">Метод <xref:System.IO.Directory.Move%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-162"><xref:System.IO.Directory.Move%2A?displayProperty=nameWithType> method</span></span><br /><br /> <span data-ttu-id="aa77a-163">Метод <xref:System.IO.DirectoryInfo.MoveTo%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-163"><xref:System.IO.DirectoryInfo.MoveTo%2A?displayProperty=nameWithType> method</span></span>|  
|<span data-ttu-id="aa77a-164">Копирование каталога</span><span class="sxs-lookup"><span data-stu-id="aa77a-164">Copy a directory</span></span>|[<span data-ttu-id="aa77a-165">Практическое руководство. Копирование каталогов</span><span class="sxs-lookup"><span data-stu-id="aa77a-165">How to: Copy Directories</span></span>](../../../docs/standard/io/how-to-copy-directories.md)|  
|<span data-ttu-id="aa77a-166">Удаление каталога</span><span class="sxs-lookup"><span data-stu-id="aa77a-166">Delete a directory</span></span>|<span data-ttu-id="aa77a-167">Метод <xref:System.IO.Directory.Delete%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-167"><xref:System.IO.Directory.Delete%2A?displayProperty=nameWithType> method</span></span><br /><br /> <span data-ttu-id="aa77a-168">Метод <xref:System.IO.DirectoryInfo.Delete%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-168"><xref:System.IO.DirectoryInfo.Delete%2A?displayProperty=nameWithType> method</span></span>|  
|<span data-ttu-id="aa77a-169">Просмотр файлов и подкаталогов в каталогах</span><span class="sxs-lookup"><span data-stu-id="aa77a-169">See the files and subdirectories in a directory</span></span>|[<span data-ttu-id="aa77a-170">Практическое руководство. Перечисление каталогов и файлов</span><span class="sxs-lookup"><span data-stu-id="aa77a-170">How to: Enumerate Directories and Files</span></span>](../../../docs/standard/io/how-to-enumerate-directories-and-files.md)|  
|<span data-ttu-id="aa77a-171">Определение размера каталога</span><span class="sxs-lookup"><span data-stu-id="aa77a-171">Find the size of a directory</span></span>|<span data-ttu-id="aa77a-172">Класс <xref:System.IO.Directory?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-172"><xref:System.IO.Directory?displayProperty=nameWithType> class</span></span>|  
|<span data-ttu-id="aa77a-173">Определение существования каталога</span><span class="sxs-lookup"><span data-stu-id="aa77a-173">Determine whether a directory exists</span></span>|<span data-ttu-id="aa77a-174">Метод <xref:System.IO.Directory.Exists%2A?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="aa77a-174"><xref:System.IO.Directory.Exists%2A?displayProperty=nameWithType> method</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="aa77a-175">См. также</span><span class="sxs-lookup"><span data-stu-id="aa77a-175">See Also</span></span>  
 [<span data-ttu-id="aa77a-176">Файловый и потоковый ввод-вывод</span><span class="sxs-lookup"><span data-stu-id="aa77a-176">File and Stream I-O</span></span>](../../../docs/standard/io/index.md)  
 [<span data-ttu-id="aa77a-177">Составление потоков</span><span class="sxs-lookup"><span data-stu-id="aa77a-177">Composing Streams</span></span>](../../../docs/standard/io/composing-streams.md)  
 [<span data-ttu-id="aa77a-178">Асинхронный файловый ввод-вывод</span><span class="sxs-lookup"><span data-stu-id="aa77a-178">Asynchronous File I/O</span></span>](../../../docs/standard/io/asynchronous-file-i-o.md)