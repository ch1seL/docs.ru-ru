---
title: "Стилизация фокуса в элементах управления и FocusVisualStyle"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- keyboard focus [WPF]
- focus [WPF], visual styling
- styles [WPF], focus visual style
ms.assetid: 786ac576-011b-4d72-913b-558deccb9b35
caps.latest.revision: "10"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: bf04af2baa037b2df9e2980cc2347460de961c39
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="styling-for-focus-in-controls-and-focusvisualstyle"></a><span data-ttu-id="e8cd2-102">Стилизация фокуса в элементах управления и FocusVisualStyle</span><span class="sxs-lookup"><span data-stu-id="e8cd2-102">Styling for Focus in Controls, and FocusVisualStyle</span></span>
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]<span data-ttu-id="e8cd2-103"> предоставляет два параллельных механизма для изменения внешнего вида элемента управления при получении фокуса клавиатуры.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-103"> provides two parallel mechanisms for changing the visual appearance of a control when it receives keyboard focus.</span></span> <span data-ttu-id="e8cd2-104">Первый механизм предполагает использование методы задания свойств для свойств, таких как <xref:System.Windows.UIElement.IsKeyboardFocused%2A> внутри стиля или шаблона, который применяется к элементу управления.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-104">The first mechanism is to use property setters for properties such as <xref:System.Windows.UIElement.IsKeyboardFocused%2A> within the style or template that is applied to the control.</span></span> <span data-ttu-id="e8cd2-105">Второй механизм заключается в предоставлении отдельного стиля в качестве значения <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A> свойства; «фокуса визуальный стиль» создает отдельное визуальное дерево для графического элемента, который рисует поверх элемента управления, вместо изменения визуального дерева элемента управления или другой пользовательский Интерфейс элемент, заменив его.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-105">The second mechanism is to provide a separate style as the value of the <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A> property; the "focus visual style" creates a separate visual tree for an adorner that draws on top of the control, rather than changing the visual tree of the control or other UI element by replacing it.</span></span> <span data-ttu-id="e8cd2-106">В данном разделе рассматриваются сценарии, для которых подходит любой из этих механизмов.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-106">This topic discusses the scenarios where each of these mechanisms is appropriate.</span></span>  
   
  
<a name="Purpose"></a>   
## <a name="the-purpose-of-focus-visual-style"></a><span data-ttu-id="e8cd2-107">Назначение визуального стиля фокуса</span><span class="sxs-lookup"><span data-stu-id="e8cd2-107">The Purpose of Focus Visual Style</span></span>  
 <span data-ttu-id="e8cd2-108">Функция визуального стиля фокуса предоставляет общую "объектную модель" для введения визуальной обратной связи с пользователем на основе навигации с помощью клавиатуры к любому элементу пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-108">The focus visual style feature provides a common "object model" for introducing visual user feedback based on keyboard navigation to any UI element.</span></span> <span data-ttu-id="e8cd2-109">Это можно сделать без применения нового шаблона к элементу управления или знания композиции определенного шаблона.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-109">This is possible without applying a new template to the control, or knowing the specific template composition.</span></span>  
  
 <span data-ttu-id="e8cd2-110">Но именно потому, что функция визуального стиля фокуса работает без знания шаблонов элементов управления, визуальная обратная связь, которая может отображаться для элемента управления с использованием визуального стиля фокуса, ограничена в обязательном порядке.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-110">However, precisely because the focus visual style feature works without knowing the control templates, the visual feedback that can be displayed for a control using a focus visual style is necessarily limited.</span></span> <span data-ttu-id="e8cd2-111">Эта функция фактически накладывает другое визуальное дерево (декоративный элемент) поверх визуального дерева, созданного при отрисовке элемента управления с помощью его шаблона.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-111">What the feature actually does is to overlay a different visual tree (an adorner) on top of the visual tree as created by a control's rendering through its template.</span></span> <span data-ttu-id="e8cd2-112">Определить это отдельное визуальное дерево с использованием стиля, который заполняет <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A> свойство.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-112">You define this separate visual tree using a style that fills the <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A> property.</span></span>  
  
<a name="Default"></a>   
## <a name="default-focus-visual-style-behavior"></a><span data-ttu-id="e8cd2-113">Поведение визуального стиля фокуса по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e8cd2-113">Default Focus Visual Style Behavior</span></span>  
 <span data-ttu-id="e8cd2-114">Визуальные стили фокуса действуют только тогда, когда действие фокусировки было инициировано клавиатурой.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-114">Focus visual styles act only when the focus action was initiated by the keyboard.</span></span> <span data-ttu-id="e8cd2-115">Любое действие мыши или программное изменение фокуса отключает режим визуальных стилей фокуса.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-115">Any mouse action or programmatic focus change disables the mode for focus visual styles.</span></span> <span data-ttu-id="e8cd2-116">Дополнительные сведения о различиях между режимами фокуса см. в разделе [Общие сведения о фокусе](../../../../docs/framework/wpf/advanced/focus-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e8cd2-116">For more information about the distinctions between focus modes, see [Focus Overview](../../../../docs/framework/wpf/advanced/focus-overview.md).</span></span>  
  
 <span data-ttu-id="e8cd2-117">Темы для элементов управления включают поведение визуального стиля фокуса по умолчанию, который становится визуальным стилем фокуса для всех элементов управления в теме.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-117">The themes for controls include a default focus visual style behavior that becomes the focus visual style for all controls in the theme.</span></span> <span data-ttu-id="e8cd2-118">Этот стиль темы определяется значением статического ключа <xref:System.Windows.SystemParameters.FocusVisualStyleKey%2A>.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-118">This theme style is identified by the value of the static key <xref:System.Windows.SystemParameters.FocusVisualStyleKey%2A>.</span></span> <span data-ttu-id="e8cd2-119">При объявлении собственного визуального стиля фокуса на уровне приложения можно заменить это поведение стиля по умолчанию из темы.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-119">When you declare your own focus visual style at the application level, you replace this default style behavior from the themes.</span></span> <span data-ttu-id="e8cd2-120">Кроме того, при определении целой темы необходимо использовать этот же ключ для определения стиля поведения по умолчанию для всей темы.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-120">Alternatively, if you define the entire theme, then you should use this same key to define the style for the default behavior for your entire theme.</span></span>  
  
 <span data-ttu-id="e8cd2-121">В темах визуальный стиль фокуса по умолчанию обычно очень прост.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-121">In the themes, the default focus visual style is generally very simple.</span></span> <span data-ttu-id="e8cd2-122">Ниже приводится приблизительная оценка.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-122">The following is a rough approximation:</span></span>  
  
```  
<Style x:Key="{x:Static SystemParameters.FocusVisualStyleKey}">  
  <Setter Property="Control.Template">  
    <Setter.Value>  
      <ControlTemplate>  
        <Rectangle StrokeThickness="1"  
          Stroke="Black"  
          StrokeDashArray="1 2"  
          SnapsToDevicePixels="true"/>  
      </ControlTemplate>  
    </Setter.Value>  
  </Setter>  
</Style>  
```  
  
<a name="When"></a>   
## <a name="when-to-use-focus-visual-styles"></a><span data-ttu-id="e8cd2-123">Когда следует использовать визуальные стили фокуса</span><span class="sxs-lookup"><span data-stu-id="e8cd2-123">When to Use Focus Visual Styles</span></span>  
 <span data-ttu-id="e8cd2-124">Концептуально внешний вид визуальных стилей фокуса, применяемых к элементам управления, должен быть согласованным в различных элементах.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-124">Conceptually, the appearance of focus visual styles applied to controls should be coherent from control to control.</span></span> <span data-ttu-id="e8cd2-125">Одним из способов обеспечить такую согласованность является изменение визуального стиля фокуса только при составлении целой темы, в которой каждый элемент управления, определенный в теме, получает либо один и тот же визуальный стиль фокуса, либо некоторую вариацию стиля, визуально связанную с другими элементами управления.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-125">One way to ensure coherence is to change the focus visual style only if you are composing an entire theme, where each control that is defined in the theme gets either the very same focus visual style, or some variation of a style that is visually related from control to control.</span></span> <span data-ttu-id="e8cd2-126">Кроме того, можно использовать один и тот же стиль (или аналогичные стили) для каждого элемента, фокусируемого с клавиатуры, на странице или в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-126">Alternatively, you might use the same style (or similar styles) to style every keyboard-focusable element on a page or in a UI.</span></span>  
  
 <span data-ttu-id="e8cd2-127">Параметр <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A> на стили отдельного элемента управления, которые не являются частью темы — не предназначены фокус визуальных стилей.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-127">Setting <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A> on individual control styles that are not part of a theme is not the intended usage of focus visual styles.</span></span> <span data-ttu-id="e8cd2-128">Это связано с тем, что несогласованность визуального поведения элементов управления может привести к путанице при использовании фокуса клавиатуры.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-128">This is because an inconsistent visual behavior between controls can lead to a confusing user experience regarding keyboard focus.</span></span> <span data-ttu-id="e8cd2-129">Если планируется поведения фокуса клавиатуры для конкретного элемента управления, намеренно не согласовано для темы гораздо лучшим подходом является использование триггеров в стилях для отдельных свойств состояния ввода, такие как <xref:System.Windows.UIElement.IsFocused%2A> или <xref:System.Windows.UIElement.IsKeyboardFocused%2A>.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-129">If you are intending control-specific behaviors for keyboard focus that are deliberately not coherent across a theme, a much better approach is to use triggers in styles for individual input state properties, such as <xref:System.Windows.UIElement.IsFocused%2A> or <xref:System.Windows.UIElement.IsKeyboardFocused%2A>.</span></span>  
  
 <span data-ttu-id="e8cd2-130">Визуальные стили фокуса действуют исключительно для фокуса клавиатуры.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-130">Focus visual styles act exclusively for keyboard focus.</span></span> <span data-ttu-id="e8cd2-131">Таким образом, визуальные стили фокуса являются функцией специальных возможностей.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-131">As such, focus visual styles are a type of accessibility feature.</span></span> <span data-ttu-id="e8cd2-132">Если требуется изменять пользовательский интерфейс для какого-либо типа фокуса с помощью мыши, клавиатуры или программными средствами, то не следует использовать визуальные стили фокуса. Вместо этого используйте методы задания и триггеры в стилях или шаблонах, которые работают на основе значения общих свойств фокуса, таких как `IsFocused` или `IsFocusWithin`.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-132">If you want UI changes for any type of focus, whether via mouse, keyboard, or programmatically, then you should not use focus visual styles, and should instead use setters and triggers in styles or templates that are working from the value of general focus properties such as `IsFocused` or `IsFocusWithin`.</span></span>  
  
<a name="How"></a>   
## <a name="how-to-create-a-focus-visual-style"></a><span data-ttu-id="e8cd2-133">Создание визуального стиля фокуса</span><span class="sxs-lookup"><span data-stu-id="e8cd2-133">How to Create a Focus Visual Style</span></span>  
 <span data-ttu-id="e8cd2-134">Стиль можно создать визуальный стиль фокуса всегда должен иметь <xref:System.Windows.Style.TargetType%2A> из <xref:System.Windows.Controls.Control>.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-134">The style you create for a focus visual style should always have the <xref:System.Windows.Style.TargetType%2A> of <xref:System.Windows.Controls.Control>.</span></span> <span data-ttu-id="e8cd2-135">Стиль должен состоять в основном из <xref:System.Windows.Controls.ControlTemplate>.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-135">The style should consist mainly of a <xref:System.Windows.Controls.ControlTemplate>.</span></span> <span data-ttu-id="e8cd2-136">Не указан целевой тип как тип, которой назначен стиль визуального отображения фокуса <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A>.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-136">You do not specify the target type to be the type where the focus visual style is assigned to the <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A>.</span></span>  
  
 <span data-ttu-id="e8cd2-137">Так как целевой тип данных — всегда <xref:System.Windows.Controls.Control>, стиля необходимо с помощью свойств, которые являются общими для всех элементов управления (с помощью свойств <xref:System.Windows.Controls.Control> класса и его базовых классов).</span><span class="sxs-lookup"><span data-stu-id="e8cd2-137">Because the target type is always <xref:System.Windows.Controls.Control>, you must style by using properties that are common to all controls (using properties of the <xref:System.Windows.Controls.Control> class and its base classes).</span></span> <span data-ttu-id="e8cd2-138">Необходимо создать шаблон, который будет правильно функционировать как наложение для элемента пользовательского интерфейса и не будет скрывать функциональные области элемента управления.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-138">You should create a template that will properly function as an overlay to a UI element and that will not obscure functional areas of the control.</span></span> <span data-ttu-id="e8cd2-139">Как правило, это означает, что визуальная обратная связь должна появляться за пределами полей управления или в качестве временных или ненавязчивых эффектов, которые не будут блокировать проверку нажатий в элементе управления, к которому применен визуальный стиль фокуса.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-139">Generally, this means that the visual feedback should appear outside the control margins, or as temporary or unobtrusive effects that will not block the hit testing on the control where the focus visual style is applied.</span></span> <span data-ttu-id="e8cd2-140">Включает свойства, которые можно использовать в шаблоне привязки полезны для определения размеров и расположения шаблона наложения <xref:System.Windows.FrameworkElement.ActualHeight%2A>, <xref:System.Windows.FrameworkElement.ActualWidth%2A>, <xref:System.Windows.FrameworkElement.Margin%2A>, и <xref:System.Windows.Controls.Control.Padding%2A>.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-140">Properties that you can use in template binding that are useful for determining sizing and positioning of your overlay template include <xref:System.Windows.FrameworkElement.ActualHeight%2A>, <xref:System.Windows.FrameworkElement.ActualWidth%2A>, <xref:System.Windows.FrameworkElement.Margin%2A>, and <xref:System.Windows.Controls.Control.Padding%2A>.</span></span>  
  
<a name="Alternatives"></a>   
## <a name="alternatives-to-using-a-focus-visual-style"></a><span data-ttu-id="e8cd2-141">Альтернативные варианты использования визуального стиля фокуса</span><span class="sxs-lookup"><span data-stu-id="e8cd2-141">Alternatives to Using a Focus Visual Style</span></span>  
 <span data-ttu-id="e8cd2-142">В ситуациях, когда использование визуального стиля фокуса нецелесообразно (при стилизации только отдельных элементов управления или если необходим больший контроль над шаблоном элемента управления), существует множество других доступных свойств и методов, которые могут создавать визуальное поведение в ответ на изменения фокуса.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-142">For situations where using a focus visual style is not appropriate, either because you are only styling single controls or because you want greater control over the control template, there are many other accessible properties and techniques that can create visual behavior in response to changes in focus.</span></span>  
  
 <span data-ttu-id="e8cd2-143">Триггеры, методы задания и методы задания событий рассматриваются подробно в разделе [Использование стилей и шаблонов](../../../../docs/framework/wpf/controls/styling-and-templating.md).</span><span class="sxs-lookup"><span data-stu-id="e8cd2-143">Triggers, setters, and event setters are all discussed in detail in [Styling and Templating](../../../../docs/framework/wpf/controls/styling-and-templating.md).</span></span> <span data-ttu-id="e8cd2-144">Обработка перенаправляемых событий рассматривается в разделе [Общие сведения о перенаправляемых событиях](../../../../docs/framework/wpf/advanced/routed-events-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e8cd2-144">Routed event handling is discussed in [Routed Events Overview](../../../../docs/framework/wpf/advanced/routed-events-overview.md).</span></span>  
  
### <a name="iskeyboardfocused"></a><span data-ttu-id="e8cd2-145">IsKeyboardFocused</span><span class="sxs-lookup"><span data-stu-id="e8cd2-145">IsKeyboardFocused</span></span>  
 <span data-ttu-id="e8cd2-146">Если вас интересуют специально фокус клавиатуры, <xref:System.Windows.UIElement.IsKeyboardFocused%2A> свойства зависимостей можно использовать для свойства <xref:System.Windows.Trigger>.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-146">If you are specifically interested in keyboard focus, the <xref:System.Windows.UIElement.IsKeyboardFocused%2A> dependency property can be used for a property <xref:System.Windows.Trigger>.</span></span> <span data-ttu-id="e8cd2-147">Триггер свойства в стиле или шаблоне является более подходящим методом определения поведения фокуса клавиатуры, который применяется только для отдельного элемента управления и может визуально не соответствовать поведению фокуса клавиатуры других элементов управления.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-147">A property trigger in either a style or template is a more appropriate technique for defining a keyboard focus behavior that is very specifically for a single control, and which might not visually match the keyboard focus behavior for other controls.</span></span>  
  
 <span data-ttu-id="e8cd2-148">Другим похожим свойством зависимостей является <xref:System.Windows.UIElement.IsKeyboardFocusWithin%2A>, который следует использовать, если требуется визуально обнаружить фокус от клавиатуры находится где-нибудь внутри композиции или функциональной области элемента управления.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-148">Another similar dependency property is <xref:System.Windows.UIElement.IsKeyboardFocusWithin%2A>, which might be appropriate to use if you want to visually call out that keyboard focus is somewhere within compositing or within the functional area of the control.</span></span> <span data-ttu-id="e8cd2-149">Например, можно поместить <xref:System.Windows.UIElement.IsKeyboardFocusWithin%2A> триггер таким образом, панели, которая группирует несколько элементов управления будет отображаться по-разному, даже если фокус клавиатуры точнее может находиться на отдельный элемент в пределах этой панели.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-149">For example, you might place an <xref:System.Windows.UIElement.IsKeyboardFocusWithin%2A> trigger such that a panel that groups several controls appears differently, even though keyboard focus might more precisely be on an individual element within that panel.</span></span>  
  
 <span data-ttu-id="e8cd2-150">Также можно использовать события <xref:System.Windows.UIElement.GotKeyboardFocus> и <xref:System.Windows.UIElement.LostKeyboardFocus> (а также их эквиваленты для предварительного просмотра).</span><span class="sxs-lookup"><span data-stu-id="e8cd2-150">You can also use the events <xref:System.Windows.UIElement.GotKeyboardFocus> and <xref:System.Windows.UIElement.LostKeyboardFocus> (as well as their Preview equivalents).</span></span> <span data-ttu-id="e8cd2-151">Эти события можно использовать в качестве основы для <xref:System.Windows.EventSetter>, или можно написать обработчики событий в коде.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-151">You can use these events as the basis for an <xref:System.Windows.EventSetter>, or you can write handlers for the events in code-behind.</span></span>  
  
### <a name="other-focus-properties"></a><span data-ttu-id="e8cd2-152">Другие свойства фокуса</span><span class="sxs-lookup"><span data-stu-id="e8cd2-152">Other Focus Properties</span></span>  
 <span data-ttu-id="e8cd2-153">Если требуется, чтобы все возможные причины изменения фокуса для создания визуального поведения, следует установить метод доступа или триггер на <xref:System.Windows.UIElement.IsFocused%2A> свойства зависимостей, либо на <xref:System.Windows.UIElement.GotFocus> или <xref:System.Windows.UIElement.LostFocus> событий, которые используются для <xref:System.Windows.EventSetter>.</span><span class="sxs-lookup"><span data-stu-id="e8cd2-153">If you want all possible causes of changing focus to produce a visual behavior, you should base a setter or trigger on the <xref:System.Windows.UIElement.IsFocused%2A> dependency property, or alternatively on the <xref:System.Windows.UIElement.GotFocus> or <xref:System.Windows.UIElement.LostFocus> events used for an <xref:System.Windows.EventSetter>.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e8cd2-154">См. также</span><span class="sxs-lookup"><span data-stu-id="e8cd2-154">See Also</span></span>  
 <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A>  
 [<span data-ttu-id="e8cd2-155">Стилизация и использование шаблонов</span><span class="sxs-lookup"><span data-stu-id="e8cd2-155">Styling and Templating</span></span>](../../../../docs/framework/wpf/controls/styling-and-templating.md)  
 [<span data-ttu-id="e8cd2-156">Общие сведения о фокусе</span><span class="sxs-lookup"><span data-stu-id="e8cd2-156">Focus Overview</span></span>](../../../../docs/framework/wpf/advanced/focus-overview.md)  
 [<span data-ttu-id="e8cd2-157">Общие сведения о входных данных</span><span class="sxs-lookup"><span data-stu-id="e8cd2-157">Input Overview</span></span>](../../../../docs/framework/wpf/advanced/input-overview.md)