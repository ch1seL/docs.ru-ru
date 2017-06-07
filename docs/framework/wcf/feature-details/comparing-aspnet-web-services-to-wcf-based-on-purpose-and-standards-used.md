---
title: "Сравнение веб-служб ASP.NET с веб-службами на основе WCF по назначению и используемым стандартам | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d3890278-fa9b-4902-91ea-8da73b7143cc
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Сравнение веб-служб ASP.NET с веб-службами на основе WCF по назначению и используемым стандартам
Веб\-службы ASP.NET были разработаны для создания приложений, которые отправляют и получают сообщения с использованием протокола SOAP \(Simple Object Access Protocol\) через HTTP.  Структуру сообщений можно определить с помощью схемы XML, а для сериализации сообщений в объекты .NET Framework и обратно предусмотрено специальное средство.  Эта технология позволяет автоматически создавать метаданные для описания веб\-служб на языке WSDL \(языке описания веб\-служб\), а второе средство предоставляется для создания клиентов для веб\-служб из WSDL.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] позволяет приложениям .NET Framework обмениваться сообщениями с другими программными сущностями.  По умолчанию используется протокол SOAP, но сообщения могут иметь любой формат и передаваться с использованием любого транспортного протокола.  Структуру сообщений можно определить с помощью схемы XML, а для сериализации сообщений в объекты .NET Framework и обратно имеется несколько параметров.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] может автоматически создавать метаданные для описания приложений, созданных с использованием этой технологии в WSDL, а также предоставляет средство для создания клиентов для этих приложений из WSDL.  
  
 Описание стандартов, поддерживаемых веб\-службами ASP.NET, приводится в документе [Веб\-службы XML, созданные с помощью ASP.NET](http://go.microsoft.com/fwlink/?LinkId=94872).  Более полный список стандартов, поддерживаемых [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], приводится в разделе [Протоколы веб\-служб, поддерживаемые предоставляемыми системой привязками](../../../../docs/framework/wcf/feature-details/web-services-protocols-supported-by-system-provided-interoperability-bindings.md).  
  
## См. также  
 [Сравнение веб\-служб ASP.NET с веб\-службами на основе WCF по процессу разработки](../../../../docs/framework/wcf/feature-details/comparing-aspnet-web-services-to-wcf-based-on-development.md)