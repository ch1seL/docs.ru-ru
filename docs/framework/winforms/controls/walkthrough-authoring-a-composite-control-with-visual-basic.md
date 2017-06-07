---
title: "Пример. Создание составного элемента управления с помощью Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "составные элементы управления, создание"
  - "элементы управления [Windows Forms], составные элементы управления"
  - "пользовательские элементы управления [Visual Basic]"
  - "пользовательские элементы управления [Windows Forms], создание"
  - "пользовательские элементы управления [Visual Basic]"
  - "пользовательские элементы управления [Windows Forms], создание с помощью Visual Basic"
  - "UserControl - класс, пошаговые руководства"
ms.assetid: f50e270e-4db2-409a-8319-6db6ca5c7daf
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Пример. Создание составного элемента управления с помощью Visual Basic
Составные элементы управления являются тем средством, с помощью которого можно создавать и многократно использовать пользовательские графические интерфейсы.  Составной элемент управления — это компонент, имеющий визуальное представление.  Он может состоять из одного или нескольких элементов управления форм Windows Forms, компонентов или блоков кода, позволяющих расширить функциональные возможности \(например, проверять допустимость вводимых пользователем данных, изменять свойства отображения или выполнять другие действия, необходимые разработчику\).  Составные элементы управления можно поместить в формы Windows Forms точно так же, как и другие элементы управления.  В первой части пошагового руководства будет создан простой составной элемент управления `ctlClock`.  Во второй части пошагового руководства функциональные возможности элемента `ctlClock` будут расширены с помощью наследования.  
  
> [!NOTE]
>  Отображаемые диалоговые окна и команды меню могут отличаться от описанных в справке в зависимости от текущих настроек или выпуска.  Чтобы изменить параметры, в меню **Сервис** выберите команду **Импорт и экспорт параметров**.  Дополнительные сведения см. в разделе [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/ru-ru/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## Создание проекта  
 При создании нового проекта следует задать его имя, чтобы были установлены корневое пространство имен, имя сборки и имя проекта, а компонент, создаваемый по умолчанию, был помещен в нужное пространство имен.  
  
#### Чтобы создать библиотеку элементов управления ctlClockLib и элемент управления ctlClock  
  
1.  В меню **Файл** выберите **Создать** и выберите пункт **Проект**, чтобы открыть диалоговое окно **Новый проект**.  
  
2.  Из списка проектов [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] выберите шаблон проекта **Библиотека элементов управления Windows** и в поле **Имя** введите `ctlClockLib`, затем нажмите кнопку **OK**.  
  
     Имя проекта \(`ctlClockLib`\) также назначается по умолчанию корневому пространству имен.  Для определения имен компонентов в сборке используется корневое пространство имен.  Например, если в двух сборках содержатся компоненты с именем `ctlClock`, то можно указать свой компонент `ctlClock`, используя имя `ctlClockLib.ctlClock.` .  
  
3.  В обозревателе решений щелкните правой кнопкой мыши файл **UserControl1.vb** и затем нажмите **Переименовать**.  Измените имя файла на `ctlClock.vb`.  Нажмите кнопку **Да**, чтобы переименовать все ссылки на элемент кода UserControl1.  
  
    > [!NOTE]
    >  По умолчанию составной компонент является наследником класса <xref:System.Windows.Forms.UserControl>, предоставляемого системой.  Класс <xref:System.Windows.Forms.UserControl> обеспечивает функциональность, необходимую всем составным элементам управления, и реализует стандартные методы и свойства.  
  
4.  В меню **Файл** выберите команду **Сохранить все** для сохранения проекта.  
  
## Добавление элементов управления и компонентов Windows в составной элемент управления  
 Визуальный интерфейс — это важная часть составного элемента управления.  Он создается путем добавления одного или нескольких элементов управления Windows на поверхность конструктора.  В приведенном ниже примере будет показано, как добавлять элементы управления Windows в составной элемент управления и реализовывать необходимые функциональные возможности с помощью написания кода.  
  
#### Чтобы добавить элементы управления Label и Timer в составной элемент управления  
  
1.  В обозревателе решений щелкните правой кнопкой мыши элемент **ctlClock.vb** и выберите пункт **Конструктор представлений**.  
  
2.  На панели элементов разверните узел **Общие элементы управления** и дважды щелкните элемент **Надпись**.  
  
     Элемент управления <xref:System.Windows.Forms.Label> с именем `Label1` будет добавлен в созданный элемент управления на поверхности конструктора.  
  
3.  Выберите в конструкторе элемент **Label1**.  В окне свойств задайте значения для следующих свойств.  
  
    |Свойство.|Значение|  
    |---------------|--------------|  
    |**Имя**|`lblDisplay`|  
    |**Текст**|`(пробел)`|  
    |**TextAlign**|`MiddleCenter`|  
    |**Font.Size**|`14`|  
  
4.  На **панели элементов** разверните узел **Компоненты** и дважды щелкните элемент **Таймер**.  
  
     Поскольку <xref:System.Windows.Forms.Timer> является компонентом, он не имеет визуального представления во время выполнения.  Поэтому он отображается не с элементами управления на поверхности конструктора, а в Конструкторе компонентов \(область в нижней части поверхности конструктора\).  
  
5.  В Конструкторе компонентов щелкните компонент **Timer1** и установите значение свойства <xref:System.Windows.Forms.Timer.Interval%2A> равным `1000`, а значение свойства <xref:System.Windows.Forms.Timer.Enabled%2A> равным `True`.  
  
     Свойство <xref:System.Windows.Forms.Timer.Interval%2A> управляет частотой тиканья компонента Timer.  Каждый раз, когда компонент `Timer1` тикает, выполняется код события `Timer1_Tick`.  Значение этого свойства — это количество миллисекунд между событиями Tick.  
  
6.  В Конструкторе компонентов дважды щелкните компонент **Timer1**, чтобы перейти к событию `Timer1_Tick` компонента `ctlClock`.  
  
7.  Измените код, как указано ниже.  Обязательно измените модификатор доступа с `Private` на `Protected`.  
  
     \[Visual Basic\]  
  
    ```  
    Protected Sub Timer1_Tick(ByVal sender As Object, ByVal e As _  
        System.EventArgs) Handles Timer1.Tick  
        ' Causes the label to display the current time.    
        lblDisplay.Text = Format(Now, "hh:mm:ss")  
    End Sub  
    ```  
  
     Этот код позволяет отобразить текущее время в элементе управления `lblDisplay`.  Поскольку интервал между событиями Tick для компонента `Timer1` был установлен равным `1000`, эти события возникают через каждую тысячу миллисекунд, то есть текущее время обновляется каждую секунду.  
  
8.  Измените этот метод, сделав его доступным для переопределения.  Дополнительные сведения см. ниже в разделе "Наследование из пользовательского элемента управления".  
  
     \[Visual Basic\]  
  
    ```  
    Protected Overridable Sub Timer1_Tick(ByVal sender As Object, ByVal _  
        e As System.EventArgs) Handles Timer1.Tick  
    ```  
  
9. В меню **Файл** выберите команду **Сохранить все** для сохранения проекта.  
  
## Добавление свойств в составной элемент управления  
 Созданный элемент управления часы теперь инкапсулирует элемент управления <xref:System.Windows.Forms.Label> и компонент <xref:System.Windows.Forms.Timer>, каждый из которых имеет собственный набор наследуемых свойств.  Хотя свойства этих элементов управления не будут доступны пользователям создаваемого элемента управления, можно создать и предоставить другим приложениям настраиваемые свойства, написав соответствующие блоки кода.  В следующей процедуре показано, как добавить в элемент управления свойства, позволяющие пользователю изменять цвет фона и текста.  
  
#### Для добавления свойства в составной элемент управления выполните следующие действия.  
  
1.  В обозревателе решений щелкните правой кнопкой мыши элемент **ctlClock.vb** и выберите пункт **Просмотреть код**.  
  
     Откроется Редактор кода для выбранного элемента управления.  
  
2.  Найдите оператор `Public Class ctlClock`.  Под ней введите следующий код.  
  
     \[Visual Basic\]  
  
    ```  
    Private colFColor as Color  
    Private colBColor as Color  
    ```  
  
     Эти операторы создают закрытые переменные. В них будут храниться значения создаваемых свойств.  
  
3.  Вставьте следующий код под объявлениями переменных, созданными на этапе 2:  
  
     \[Visual Basic\]  
  
    ```  
    ' Declares the name and type of the property.  
    Property ClockBackColor() as Color  
        ' Retrieves the value of the private variable colBColor.  
        Get  
            Return colBColor  
        End Get  
        ' Stores the selected value in the private variable colBColor, and   
        ' updates the background color of the label control lblDisplay.  
        Set(ByVal value as Color)  
            colBColor = value  
            lblDisplay.BackColor = colBColor     
        End Set  
  
    End Property  
    ' Provides a similar set of instructions for the foreground color.  
    Property ClockForeColor() as Color  
        Get  
            Return colFColor  
        End Get  
        Set(ByVal value as Color)  
            colFColor = value  
            lblDisplay.ForeColor = colFColor  
        End Set  
    End Property  
    ```  
  
     Приведенный выше код позволяет пользователям этого элемента управления получить доступ к настраиваемым свойствам `ClockForeColor` и `ClockBackColor` с помощью вызова оператора `Property`.  Операторы `Get` и `Set` соответственно сохраняют и извлекают значение свойства, а также выполняют код, реализующий необходимую функцию.  
  
4.  В меню **Файл** выберите команду **Сохранить все** для сохранения проекта.  
  
## Проверка элемента управления  
 Элементы управления не являются автономными проектами; они должны быть включены в контейнер.  Проверьте поведение созданного элемента управления и испытайте его свойства с помощью **Тестового контейнера пользовательских элементов управления**.  Дополнительные сведения см. в разделе [Практическое руководство. Тестирование поведения элемента UserControl во время выполнения](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md).  
  
#### Чтобы протестировать элемент управления  
  
1.  Нажмите клавишу F5 для построения проекта и запустите элемент управления в **Тестовом контейнере пользовательских элементов управления**.  
  
2.  В таблице свойств тестового контейнера выберите свойство `ClockBackColor` и щелкните стрелку выпадающего меню, чтобы вывести на экран цветовую палитру.  
  
3.  Выберите цвет с помощью щелчка мыши.  
  
     Цвет фона элемента управления изменится на выбранный цвет.  
  
4.  С помощью аналогичной последовательности событий проверьте, что свойство `ClockForeColor` работает правильно.  
  
5.  Нажмите кнопку **Закрыть**, чтобы закрыть окно **Тестового контейнера пользовательских элементов управления**.  
  
     В этом и предыдущем разделе было показано, как компоненты и элементы управления Windows можно объединить с кодом и упаковкой, чтобы предоставить пользовательские функциональные возможности в виде составного элемента управления.  Было продемонстрировано, как предоставлять свойства составного элемента управления и тестировать элемент управления после завершения его разработки.  В следующем разделе содержатся сведения о построении наследуемого составного элемента управления на базе элемента управления `ctlClock`.  
  
## Наследование из составного элемента управления  
 В предыдущих разделах рассказывалось, как объединить компоненты, элементы управления Windows и код, чтобы создать составные элементы управления, доступные для многократного использования.  В этом разделе будет показано, как на основе составного элемента управления построить другие элементы управления.  Процесс создания производного класса на основе базового класса называется *наследованием*.  В этом разделе будет создан составной элемент управления `ctlAlarmClock`.  Он будет производным от родительского элемента управления `ctlClock`.  Также будет показано, как расширить функциональные возможности элемента `ctlClock` путем переопределения методов родительского класса и добавления новых методов и свойств.  
  
 Первым шагом для создания наследуемого элемента управления является наследование от родительского элемента управления.  При этом создается новый элемент управления, который не только имеет все свойства, методы и графические характеристики родительского элемента управления, но и служит основой для добавления или изменения функциональных возможностей.  
  
#### Чтобы создать наследуемый элемент управления  
  
1.  В обозревателе решений щелкните проект правой кнопкой мыши элемент **ctlClockLib**, укажите **Добавить** и выберите **Пользовательский элемент управления**.  
  
     Откроется диалоговое окно **Добавление нового элемента**.  
  
2.  Выберите шаблон **Наследуемый пользовательский элемент управления**.  
  
3.  В поле **Имя** введите `ctlAlarmClock.vb` и нажмите кнопку **Добавить**.  
  
     Откроется диалоговое окно **Выбор компонентов для наследования**.  
  
4.  Дважды щелкните **ctlClock** под строкой **Имя компонента**.  
  
5.  В обозревателе решений просмотрите список текущих проектов.  
  
    > [!NOTE]
    >  В текущий проект был добавлен файл **ctlAlarmClock.vb**.  
  
### Добавление свойств будильника  
 Добавление свойств в наследуемый элемент управления выполняется точно так же, как и в случае с составным элементом управления.  Теперь будет использован синтаксис объявления свойства для добавления двух свойств в элемент управления: `AlarmTime`, хранящее значение даты и времени срабатывания будильника, и `AlarmSet`, показывающее, установлен ли будильник.  
  
##### Для добавления свойств в составной элемент управления выполните следующие действия.  
  
1.  В обозревателе решений щелкните правой кнопкой мыши элемент **ctlAlarmClock** и выберите пункт **Просмотреть код**.  
  
2.  Найдите объявление класса элемента управления ctlAlarmClock, которое выглядит как `Public Class ctlAlarmClock`.  Добавьте в объявление класса следующий код.  
  
     \[Visual Basic\]  
  
    ```  
    Private dteAlarmTime As Date  
    Private blnAlarmSet As Boolean  
    ' These properties will be declared as Public to allow future   
    ' developers to access them.  
    Public Property AlarmTime() As Date  
        Get  
            Return dteAlarmTime  
        End Get  
        Set(ByVal value as Date)  
            dteAlarmTime = value  
        End Set  
    End Property  
    Public Property AlarmSet() As Boolean  
        Get  
            Return blnAlarmSet  
        End Get  
        Set(ByVal value as Boolean)  
            blnAlarmSet = value  
        End Set  
    End Property  
    ```  
  
### Добавление графического интерфейса в элемент управления  
 Наследуемый элемент управления имеет такой же визуальный интерфейс, как и его родительский элемент управления.  Наследуемый элемент управления также наследует все элементы управления, содержащиеся в родительском элементе управления, но их свойства недоступны из наследуемого элемента, если они не были предоставлены явным образом.  В графический интерфейс наследуемого составного элемента управления можно добавлять элементы так же, как и в графический интерфейс любого другого составного элемента управления.  Далее в визуальный интерфейс будильника будет добавлен элемент управления надпись, который будет мигать при срабатывании будильника.  
  
##### Чтобы добавить элемент управления надпись  
  
1.  В обозревателе решений щелкните правой кнопкой мыши элемент **ctlAlarmClock** и выберите пункт **Конструктор представлений**.  
  
     В главном окне откроется конструктор элемента управления `ctlAlarmClock`.  
  
2.  Щелкните `lblDisplay` \(область отображения элемента управления\) и изучите окно "Свойства".  
  
    > [!NOTE]
    >  Хотя все свойства отображаются, они затенены.  Это означает, что эти свойства являются собственными свойствами для `lblDisplay` и в окне свойств нельзя ни изменить их, ни обратиться к ним.  Элементы управления, содержащиеся в составном элементе управления, по умолчанию являются закрытыми \(`Private`\), и их свойства недоступны.  
  
    > [!NOTE]
    >  Чтобы пользователи элемента управления имели доступ к его внутренним элементам управления, эти элементы управления должны быть объявлены как `Public` или `Protected`.  Это позволит устанавливать и изменять свойства элементов управления, содержащихся в составном элементе управления, с помощью написания соответствующего кода.  
  
3.  Для добавления элемента управления <xref:System.Windows.Forms.Label> в составной элемент управления выполните следующие действия.  
  
4.  С помощью мыши перетащите элемент управления <xref:System.Windows.Forms.Label> непосредственно под поле отображения.  В окне свойств задайте значения для следующих свойств.  
  
    |Свойство.|Параметр|  
    |---------------|--------------|  
    |**Имя**|`lblAlarm`|  
    |**Текст**|Будильник\!|  
    |**TextAlign**|`MiddleCenter`|  
    |**Visible**|`False`|  
  
### Добавление функциональных возможностей будильника  
 Свойства и элемент управления, добавленные в предыдущих процедурах, позволяют реализовать функциональные возможности будильника в составном элементе управления.  В этой процедуре в пользовательский элемент управления будет добавлен код, в котором текущее время сравнивается со временем срабатывания будильника. Если они совпадают, будильник начинает звонить и мигать.  Переопределив метод `Timer1_Tick` элемента управления `ctlClock`и добавив в него дополнительный код, можно расширить функциональные возможности наследуемого элемента управления `ctlAlarmClock`, сохранив в то же время все функциональные возможности элемента `ctlClock`.  
  
##### Чтобы переопределить метод Timer1\_Tick компонента ctlClock  
  
1.  В обозревателе решений щелкните правой кнопкой мыши элемент **ctlAlarmClock.vb** и выберите пункт **Просмотреть код**.  
  
2.  Найдите оператор `Private blnAlarmSet As Boolean`.  Непосредственно после него добавьте следующий оператор.  
  
     \[Visual Basic\]  
  
    ```  
    Dim blnColorTicker as Boolean  
    ```  
  
3.  В нижней части страницы найдите оператор `End Class`.  Непосредственно перед оператором `End Class` добавьте следующий код.  
  
     \[Visual Basic\]  
  
    ```  
    Protected Overrides Sub Timer1_Tick(ByVal sender As Object, ByVal e _  
        As System.EventArgs)  
        ' Calls the Timer1_Tick method of ctlClock.  
        MyBase.Timer1_Tick(sender, e)  
        ' Checks to see if the Alarm is set.  
        If AlarmSet = False Then  
            Exit Sub  
        End If  
        ' If the date, hour, and minute of the alarm time are the same as  
        ' now, flash and beep an alarm.   
        If AlarmTime.Date = Now.Date And AlarmTime.Hour = Now.Hour And _  
            AlarmTime.Minute = Now.Minute Then  
            ' Sounds an audible beep.  
            Beep()  
            ' Sets lblAlarmVisible to True, and changes the background color based on the   
            ' value of blnColorTicker. The background color of the label will   
            ' flash once per tick of the clock.  
            lblAlarm.Visible = True  
            If blnColorTicker = False Then  
                lblAlarm.BackColor = Color.PeachPuff  
                blnColorTicker = True  
            Else  
                lblAlarm.BackColor = Color.Plum  
                blnColorTicker = False  
            End If  
        Else  
            ' Once the alarm has sounded for a minute, the label is made   
            ' invisible again.  
            lblAlarm.Visible = False  
        End If  
    End Sub  
    ```  
  
     Этот код выполняет несколько задач.  Оператор `Overrides` указывает, что элемент управления должен использовать этот метод вместо метода, унаследованного от базового элемента управления.  При вызове этого метода он вызывает переопределяемый им метод \(с помощью вызова оператора `MyBase.Timer1_Tick`\). Благодаря этому все функциональные возможности исходного элемента управления реализуются и в этом элементе.  Затем выполняется дополнительный код, реализующий функциональные возможности будильника.  При наступлении времени срабатывания будильника появится мигающий элемент управления "Надпись" и раздастся звуковой сигнал.  
  
    > [!NOTE]
    >  Обратите внимание, что при переопределении наследуемого обработчика событий событие с ключевым словом `Handles` указывать не требуется.  Это событие уже подключено.  Требуется переопределить только реализацию обработчика.  
  
     Теперь разработка будильника почти завершена.  Необходимо только реализовать возможность его отключения.  Для этого необходимо добавить код в метод `lblAlarm_Click`.  
  
##### Чтобы реализовать метод отключения будильника  
  
1.  В обозревателе решений щелкните правой кнопкой мыши элемент **ctlAlarmClock.vb** и выберите пункт **Конструктор представлений**.  
  
2.  В конструкторе дважды щелкните компонент **lblAlarm**.  В **Редакторе кода** откроется строка `Private Sub lblAlarm_Click`.  
  
3.  Измените этот метод, как указано ниже.  
  
     \[Visual Basic\]  
  
    ```  
    Private Sub lblAlarm_Click(ByVal sender As Object, ByVal e As _  
     System.EventArgs) Handles lblAlarm.Click  
        ' Turns off the alarm.  
        AlarmSet = False  
        ' Hides the flashing label.  
        lblAlarm.Visible = False  
    End Sub  
    ```  
  
4.  В меню **Файл** выберите команду **Сохранить все** для сохранения проекта.  
  
### Использование наследуемого элемента управления в форме  
 Проверить наследуемый элемент управления можно таким же образом, как был проверен элемент управления базового класса, `ctlClock`: нажмите клавишу F5 для построения проекта и напустите элемент управления в **Тестовом контейнере пользовательских элементов управления**.  Дополнительные сведения см. в разделе [Практическое руководство. Тестирование поведения элемента UserControl во время выполнения](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md).  
  
 Для использования элемента управления необходимо включить его в форму.  Как и стандартный составной элемент управления, наследуемый составной элемент управления не может быть автономным и должен быть включен в форму или другой контейнер.  Поскольку элемент управления `ctlAlarmClock` имеет дополнительные функциональные возможности, для его тестирования требуется дополнительный код.  В этой процедуре будет написана простая программа для проверки функциональных возможностей элемента управления `ctlAlarmClock`.  Она будет устанавливать и отображать значение свойства `AlarmTime` элемента `ctlAlarmClock` и тестировать его функции.  
  
##### Чтобы построить элемент управления и добавить его в тестовую форму  
  
1.  В обозревателе решений щелкните правой кнопкой мыши **ctlClockLib** и затем выберите **Построить**.  
  
2.  В меню **Файл** выберите **Добавить**, затем **Новый проект**.  
  
3.  Добавьте в решение новый проект **Приложение Windows** и назовите его `Test`.  
  
     Проект **Test** будет добавлен в обозреватель решений.  
  
4.  Щелкните правой кнопкой мыши узел проекта `Test` в обозревателе решений и выберите пункт **Добавить ссылку**, чтобы открыть диалоговое окно **Добавление ссылки**.  
  
5.  Перейдите на вкладку **Проекты**.  Под строкой **Имя проекта** можно будет увидеть проект **ctlClockLib**.  Дважды щелкните **ctlClockLib**, чтобы добавить ссылку на тестовый проект.  
  
6.  В обозревателе решений щелкните правой кнопкой мыши **Test** и затем выберите **Построить**.  
  
7.  На **панели элементов** разверните узел **Компоненты ctlClockLib**.  
  
8.  Дважды щелкните **ctlAlarmClock**, чтобы добавить экземпляр `ctlAlarmClock` в форму.  
  
9. На **панели элементов** найдите элемент **DateTimePicker** и дважды щелкните его, чтобы добавить элемент управления <xref:System.Windows.Forms.DateTimePicker> в форму, а затем добавьте элемент управления <xref:System.Windows.Forms.Label>, дважды щелкнув элемент **Надпись**.  
  
10. С помощью мыши удобно расположите элементы управления в форме.  
  
11. Установите свойства этих элементов управления следующим образом.  
  
    |Элемент управления|Свойство.|Значение|  
    |------------------------|---------------|--------------|  
    |`label1`|**Текст**|`(пробел)`|  
    ||**Имя**|`lblTest`|  
    |`dateTimePicker1`|**Имя**|`dtpTest`|  
    ||**Format**|<xref:System.Windows.Forms.DateTimePickerFormat>|  
  
12. В конструкторе дважды щелкните компонент **dtpTest**.  
  
     В **редакторе кода** откроется `Private Sub dtpTest_ValueChanged`.  
  
13. Измените код, как показано ниже.  
  
     \[Visual Basic\]  
  
    ```  
    Private Sub dtpTest_ValueChanged(ByVal sender As Object, ByVal e As _  
        System.EventArgs) Handles dtpTest.ValueChanged  
        ctlAlarmClock1.AlarmTime = dtpTest.Value  
        ctlAlarmClock1.AlarmSet = True  
        lblTest.Text = "Alarm Time is " & Format(ctlAlarmClock1.AlarmTime, _  
            "hh:mm")  
    End Sub  
    ```  
  
14. В обозревателе решений щелкните правой кнопкой мыши **Test** и выберите **Назначить автозагружаемым проектом**.  
  
15. В меню **Отладка** щелкните **Начать отладку**.  
  
     Начнется выполнение тестовой программы.  Обратите внимание, что в элементе управления `ctlAlarmClock` отображается текущее время \(которое постоянно обновляется\), а в элементе управления <xref:System.Windows.Forms.DateTimePicker> — начальное время.  
  
16. Щелкните поле элемента <xref:System.Windows.Forms.DateTimePicker>, в котором отображаются минуты.  
  
17. С помощью клавиатуры измените значение этого поля таким образом, чтобы оно было на одну минуту больше текущего времени, отображаемого элементом `ctlAlarmClock`.  
  
     Время включения будильника показано в элементе `lblTest`.  Дождитесь, когда текущее время станет равным времени срабатывания будильника.  В этот момент раздастся звуковой сигнал и элемент `lblAlarm` начнет мигать.  
  
18. Отключите будильник, нажав `lblAlarm`.  Теперь можно переустановить будильник.  
  
     В этом пошаговом руководстве был проиллюстрирован ряд ключевых положений.  В частности, в нем было показано, как создавать составной элемент управления посредством объединения элементов управления и компонентов в контейнер составного элемента управления.  Также было описано, как добавлять свойства в элемент управления и писать код, реализующий пользовательские функциональные возможности.  В последнем разделе было продемонстрировано, как расширять функциональные возможности составного элемента управления с помощью наследования и как изменять функциональные возможности базового элемента управления посредством переопределения методов.  
  
## См. также  
 [Создание собственных элементов управления](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)   
 [Практическое руководство. Создание составных элементов управления](../../../../docs/framework/winforms/controls/how-to-author-composite-controls.md)   
 [Практическое руководство. Отображение элемента управления в диалоговом окне выбора элементов панели элементов](../../../../docs/framework/winforms/controls/how-to-display-a-control-in-the-choose-toolbox-items-dialog-box.md)   
 [Component Authoring Walkthroughs](../Topic/Component%20Authoring%20Walkthroughs.md)