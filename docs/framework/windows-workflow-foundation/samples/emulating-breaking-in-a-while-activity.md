---
title: Эмуляция прерывания в действии While
ms.date: 03/30/2017
ms.assetid: ddff715d-d623-4b54-b841-60bacbc3ca21
ms.openlocfilehash: 4938e07364609520f6528688877bce112be26d3f
ms.sourcegitcommit: c7f3e2e9d6ead6cc3acd0d66b10a251d0c66e59d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/09/2018
ms.locfileid: "44253303"
---
# <a name="emulating-breaking-in-a-while-activity"></a>Эмуляция прерывания в действии While
Этот образец показывает, как прервать циклический механизм следующих действий: <xref:System.Activities.Statements.DoWhile>, <xref:System.Activities.Statements.ForEach%601>, <xref:System.Activities.Statements.While> и <xref:System.Activities.Statements.ParallelForEach%601>.  
  
 Это полезно, поскольку Windows Workflow Foundation (WF) не включает действия для прерывания выполнения этих циклов.  
  
## <a name="scenario"></a>Сценарий  
 Образец находит первого надежного поставщика из списка поставщиков (экземпляры класса `Vendor`). Каждый поставщик имеет `ID`, `Name` и числовое значение надежности, определяющее, насколько на его продукцию можно положиться. Образец создает пользовательское действие с именем `FindReliableVendor`, получающее два входных параметра (список поставщиков и минимальное значение надежности) и возвращает первого поставщика из списка, соответствующего предоставленным критериям.  
  
## <a name="breaking-a-loop"></a>Прерывание цикла  
 Windows Workflow Foundation (WF) не включены действия для прерывания цикла. Образец кода выполняет прерывание цикла с помощью действия <xref:System.Activities.Statements.If> и нескольких переменных. В этом образце действие <xref:System.Activities.Statements.While> прерывается, если переменной `reliableVendor` присваивается значение, отличное от `null`.  
  
 Следующий пример кода демонстрирует, как этот образец прерывает цикл while.  
  
```csharp  
// Iterates while the "i" variable is lower than the size of the list   
// and any reliable Vendor is found.        
new While(env => i.Get(env) < this.Vendors.Get(env).Count && reliableVendor.Get(env) == null)  
{  
    DisplayName = "Main loop. Breaks when a reliable vendor is found",  
    Body = new Sequence  
    {                              
        Activities =  
        {  
            // This is the if used for setting the value of the break value…  
            new If  
            {  
                DisplayName = "Check for a reliable vendor",  
  
                //  If a vendor satisfies the reliability level…  
                Condition = new InArgument<bool>(env =>   
                           this.Vendors.Get(env)[i.Get(env)].Reliability >   
                           this.MinimumReliability.Get(env)),  
  
                // then assign that vendor to the reliable vendor variable and   
                // the while condition becomes false (exit the loop).  
                Then = new Assign<Vendor>  
                {  
                    To = reliableVendor,  
                    Value = new InArgument<Vendor>(env =>   
                                  this.Vendors.Get(env)[i.Get(env)])  
                }  
            },  
  
            // Increment the iteration variable.   
            new Assign<int>  
            {  
                DisplayName = "Increment iteration variable",  
                To = i,  
                Value = new InArgument<int>(env => i.Get(env) + 1)  
            }   
        }  
    }  
}  
```  
  
#### <a name="to-use-this-sample"></a>Использование этого образца  
  
1.  Откройте файл решения EmulatingBreakInWhile.sln с помощью [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Для построения решения нажмите CTRL+SHIFT+B.  
  
3.  Чтобы запустить решение, нажмите клавиши CTRL+F5.  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере. Перед продолжением проверьте следующий каталог (по умолчанию).  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите к [Windows Communication Foundation (WCF) и образцы Windows Workflow Foundation (WF) для .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) для загрузки всех Windows Communication Foundation (WCF) и [!INCLUDE[wf1](../../../../includes/wf1-md.md)] примеры. Этот образец расположен в следующем каталоге.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Built-InActivities\EmulatingBreakInWhile`