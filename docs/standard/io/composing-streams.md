---
title: Составление потоков
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- streams, base streams
- I/O [.NET Framework], composing streams
- Stream class, composing streams
- base streams
- streams, backing stores
ms.assetid: da761658-a535-4f26-a452-b30df47f73d5
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 5e52b827f337892c33ec61b9affa1cc646a759c5
ms.sourcegitcommit: ad99773e5e45068ce03b99518008397e1299e0d1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/22/2018
ms.locfileid: "46577026"
---
# <a name="composing-streams"></a>Составление потоков
Резервное хранилище — это устройство хранения информации, например диск или память. Каждое из резервных хранилищ использует собственную реализацию потока, основанную на классе <xref:System.IO.Stream>. Каждый тип потока считывает и записывает байты в собственное резервное хранилище. Потоки, которые связаны с резервными хранилищами, называются базовыми. Базовые потоки имеют конструкторы, которые используют параметры для подключения к соответствующему резервному хранилищу. Например, конструкторы класса <xref:System.IO.FileStream> задают параметр пути, который определяет порядок совместного использования этого файла в процессах.  
  
 В структуре классов <xref:System.IO> реализовано упрощенное составление потоков. Базовые потоки могут присоединяться к одному или нескольким транзитным потокам, которые предоставляют нужные возможности. В конце цепочки можно прикрепить средство чтения или записи, что позволяет удобно читать и записывать нужные типы.  
  
 В следующем примере кода создается поток **FileStream** на основе существующего `MyFile.txt`, предназначенный для буферизации `MyFile.txt`. (Обратите внимание, что потоки **FileStream** буферизуются по умолчанию.) Далее создается <xref:System.IO.StreamReader> для чтения символов из **FileStream** и передается в качестве аргумента конструктору **StreamReader**. <xref:System.IO.StreamReader.ReadLine%2A> выполняет чтение, пока <xref:System.IO.StreamReader.Peek%2A> обнаруживает символы.  
  
 [!code-cpp[System.IO.StreamReader#20](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.StreamReader/CPP/source2.cpp#20)]
 [!code-csharp[System.IO.StreamReader#20](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.StreamReader/CS/source2.cs#20)]
 [!code-vb[System.IO.StreamReader#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.StreamReader/VB/source2.vb#20)]  
  
 В следующем примере кода создается поток **FileStream** на основе существующего `MyFile.txt`, предназначенный для буферизации `MyFile.txt`. (Обратите внимание, что потоки **FileStream** буферизуются по умолчанию.) Далее создается **BinaryReader** для чтения байтов из **FileStream** и передается в качестве аргумента конструктору **BinaryReader**. <xref:System.IO.BinaryReader.ReadByte%2A> выполняет чтение, пока <xref:System.IO.BinaryReader.PeekChar%2A> обнаруживает байты.  
  
 [!code-cpp[System.IO.StreamReader#21](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.StreamReader/CPP/source3.cpp#21)]
 [!code-csharp[System.IO.StreamReader#21](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.StreamReader/CS/source3.cs#21)]
 [!code-vb[System.IO.StreamReader#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.StreamReader/VB/source3.vb#21)]  
  
## <a name="see-also"></a>См. также

- <xref:System.IO.StreamReader>  
- <xref:System.IO.StreamReader.ReadLine%2A?displayProperty=nameWithType>  
- <xref:System.IO.StreamReader.Peek%2A?displayProperty=nameWithType>  
- <xref:System.IO.FileStream>  
- <xref:System.IO.BinaryReader>  
- <xref:System.IO.BinaryReader.ReadByte%2A?displayProperty=nameWithType>  
- <xref:System.IO.BinaryReader.PeekChar%2A?displayProperty=nameWithType>
