---
title: Практическое руководство. Переназначение существующих элементов управления другим родительским элементам
ms.date: 03/30/2017
helpviewer_keywords:
- container controls [Windows Forms], Windows Forms
- layout [Windows Forms], resizing
- layout [Windows Forms], child controls
ms.assetid: 5a5723ff-34e0-4b6f-a57b-be4ebe35cb34
ms.openlocfilehash: 77246aaf2fdaa79ad986366e39ff98a9d0f5fb50
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43513203"
---
# <a name="how-to-reassign-existing-controls-to-a-different-parent"></a>Практическое руководство. Переназначение существующих элементов управления другим родительским элементам
Можно назначать существующие в форме элементы управления новому контейнерному элементу управления.  
  
> [!NOTE]
>  Отображаемые диалоговые окна и команды меню могут отличаться от описанных в справке в зависимости от текущих параметров или выпуска. Чтобы изменить параметры, выберите в меню **Сервис** пункт **Импорт и экспорт параметров** . Дополнительные сведения см. в разделе [Персонализация интегрированной среды разработки Visual Studio](/visualstudio/ide/personalizing-the-visual-studio-ide).  
  
### <a name="to-reassign-existing-controls-to-a-different-parent"></a>Переназначение существующих элементов управления другим родительским элементам  
  
1.  Перетащите три элемента управления <xref:System.Windows.Forms.Button> с **панели элементов** в форму.  
  
     Расположите их рядом друг с другом, но не выравнивайте.  
  
2.  В **панели элементов**щелкните значок элемента управления <xref:System.Windows.Forms.FlowLayoutPanel> .  
  
     Не перетаскивайте значок на форму.  
  
3.  Переместите указатель мыши к трем элементам управления <xref:System.Windows.Forms.Button> .  
  
     Указатель превратится в перекрестие с прикрепленным значком элемента управления <xref:System.Windows.Forms.FlowLayoutPanel> .  
  
4.  Нажмите и удерживайте кнопку мыши.  
  
5.  Перемещайте указатель мыши, чтобы нарисовать контур элемента управления <xref:System.Windows.Forms.FlowLayoutPanel> .  
  
6.  Обведите таким образом три элемента управления <xref:System.Windows.Forms.Button> .  
  
7.  Отпустите кнопку мыши.  
  
     Теперь три элемента управления <xref:System.Windows.Forms.Button> вставлены в элемент управления <xref:System.Windows.Forms.FlowLayoutPanel> .  
  
## <a name="see-also"></a>См. также  
 <xref:System.Windows.Forms.FlowLayoutPanel>  
 <xref:System.Windows.Forms.TableLayoutPanel>  
 [Упорядочение элементов управления в формах Windows Forms](../../../../docs/framework/winforms/controls/arranging-controls-on-windows-forms.md)  
 [Пошаговое руководство. Упорядочение элементов управления в формах Windows Forms с помощью элемента TableLayoutPanel](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)  
 [Пример. Упорядочение элементов управления в формах Windows Forms с помощью линий привязки](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)
