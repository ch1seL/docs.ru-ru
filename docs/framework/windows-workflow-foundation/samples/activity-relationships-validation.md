---
title: Проверка связей действий
ms.date: 03/30/2017
ms.assetid: 6f11a34e-ed67-4bce-88ce-7e96bbb4d052
ms.openlocfilehash: 50f08118fb5ad4d9b8fe809e7ab3cc5d57f28149
ms.sourcegitcommit: c7f3e2e9d6ead6cc3acd0d66b10a251d0c66e59d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/08/2018
ms.locfileid: "44193670"
---
# <a name="activity-relationships-validation"></a>Проверка связей действий
Этот образец состоит из трех действий: `CreateCity`, `CreateState` и `CreateCountry`. Действие `CreateCity` должно быть внутри действия `CreateState`, а `CreateState` должно быть внутри действия `CreateCountry`. Для этого образца логика проверки реализуется в коде для действия `CreateState` и в XAML для действия `CreateCity`. Оба ограничения имеют одинаковое поведение.  
  
 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] предоставляет следующие три вспомогательных действия, которые позволяют разработчику проверять связи между действиями.  
  
 <xref:System.Activities.Validation.GetParentChain>  
 Предоставляет коллекцию из всех действий, принадлежащих родительскому узлу текущего узла.  
  
 <xref:System.Activities.Validation.GetChildSubtree>  
 Предоставляет коллекцию из всех действий, принадлежащих поддереву текущего узла, за исключением самого текущего узла.  
  
 <xref:System.Activities.Validation.GetWorkflowTree>  
 Предоставляет коллекцию из всех действий в том же дереве, что и текущий узел.  
  
 В образце действие <xref:System.Activities.Statements.ForEach%601> используется для прохождения коллекции, возвращаемой действием <xref:System.Activities.Validation.GetParentChain>. Тип каждого элемента в коллекции сравнивается с типом результата действия `CreateCountry` (или действия `CreateState`, если проверяется `CreateCity`), а после нахождения соответствия флаг результата устанавливается в `true`. Наконец <xref:System.Activities.Validation.AssertValidation> используется для формирования ошибки проверки, если флаг результата установлен в `false`.  
  
### <a name="to-use-this-sample"></a>Использование этого образца  
  
1.  Откройте образец решения ContainmentValidation.sln в [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Постройте решение.  
  
3.  Чтобы запустить программу, нажмите сочетание клавиш CTRL+F5.  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере. Перед продолжением проверьте следующий каталог (по умолчанию).  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите к [Windows Communication Foundation (WCF) и образцы Windows Workflow Foundation (WF) для .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) для загрузки всех Windows Communication Foundation (WCF) и [!INCLUDE[wf1](../../../../includes/wf1-md.md)] примеры. Этот образец находится в следующем каталоге:  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Validation\ActivityRelationships`
