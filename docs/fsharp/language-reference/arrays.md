---
title: "Массивы (F#)"
description: "Узнайте, как создать и использовать массивы в языке F #."
keywords: "visual f#, f#, функциональное программирование"
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 61fa9084-abdc-4cf5-8213-91ec1211866b
ms.openlocfilehash: 7c9d8405230f4d765d3afdeaa154ddc598d0d1ec
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="arrays"></a><span data-ttu-id="ba69f-104">Массивы</span><span class="sxs-lookup"><span data-stu-id="ba69f-104">Arrays</span></span>

> [!NOTE]
<span data-ttu-id="ba69f-105">Ссылка на справочник по API ведет на сайт MSDN.</span><span class="sxs-lookup"><span data-stu-id="ba69f-105">The API reference link will take you to MSDN.</span></span>  <span data-ttu-id="ba69f-106">Работа над справочником по API docs.microsoft.com не завершена.</span><span class="sxs-lookup"><span data-stu-id="ba69f-106">The docs.microsoft.com API reference is not complete.</span></span>

<span data-ttu-id="ba69f-107">Массивы — это коллекции фиксированного размера, отсчитываемый от нуля, изменяемых элементов данных, имеющих тот же тип.</span><span class="sxs-lookup"><span data-stu-id="ba69f-107">Arrays are fixed-size, zero-based, mutable collections of consecutive data elements that are all of the same type.</span></span>

## <a name="creating-arrays"></a><span data-ttu-id="ba69f-108">Создание массивов</span><span class="sxs-lookup"><span data-stu-id="ba69f-108">Creating Arrays</span></span>
<span data-ttu-id="ba69f-109">Массивы можно создать несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="ba69f-109">You can create arrays in several ways.</span></span> <span data-ttu-id="ba69f-110">Небольшой массив можно создать, указав последовательные значения между `[|` и `|]` и через точку с запятой, как показано в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="ba69f-110">You can create a small array by listing consecutive values between `[|` and `|]` and separated by semicolons, as shown in the following examples.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet1.fs)]

<span data-ttu-id="ba69f-111">Можно также перевести каждый элемент в отдельной строке, в котором регистр точку с запятой является необязательным.</span><span class="sxs-lookup"><span data-stu-id="ba69f-111">You can also put each element on a separate line, in which case the semicolon separator is optional.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet2.fs)]

<span data-ttu-id="ba69f-112">Тип элементов массива определяется исходя из использование литералов и должны быть согласованы.</span><span class="sxs-lookup"><span data-stu-id="ba69f-112">The type of the array elements is inferred from the literals used and must be consistent.</span></span> <span data-ttu-id="ba69f-113">Следующий код вызывает ошибку, поскольку 1.0 значение с плавающей запятой и 2 и 3 являются целыми числами.</span><span class="sxs-lookup"><span data-stu-id="ba69f-113">The following code causes an error because 1.0 is a float and 2 and 3 are integers.</span></span>

```fsharp
// Causes an error.
// let array2 = [| 1.0; 2; 3 |]
```

<span data-ttu-id="ba69f-114">Можно также использовать выражения последовательности для создания массивов.</span><span class="sxs-lookup"><span data-stu-id="ba69f-114">You can also use sequence expressions to create arrays.</span></span> <span data-ttu-id="ba69f-115">Ниже приведен пример, в котором создается массив квадратов целых чисел от 1 до 10.</span><span class="sxs-lookup"><span data-stu-id="ba69f-115">Following is an example that creates an array of squares of integers from 1 to 10.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet3.fs)]

<span data-ttu-id="ba69f-116">Для создания массива, в которой все элементы инициализируются значением 0, используйте `Array.zeroCreate`.</span><span class="sxs-lookup"><span data-stu-id="ba69f-116">To create an array in which all the elements are initialized to zero, use `Array.zeroCreate`.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet4.fs)]
    
## <a name="accessing-elements"></a><span data-ttu-id="ba69f-117">Доступ к элементам</span><span class="sxs-lookup"><span data-stu-id="ba69f-117">Accessing Elements</span></span>

<span data-ttu-id="ba69f-118">Доступ к элементам массива с помощью оператора точки (`.`) и квадратных скобок (`[` и `]`).</span><span class="sxs-lookup"><span data-stu-id="ba69f-118">You can access array elements by using a dot operator (`.`) and brackets (`[` and `]`).</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet5.fs)]

<span data-ttu-id="ba69f-119">Индексы массива начинаются с 0.</span><span class="sxs-lookup"><span data-stu-id="ba69f-119">Array indexes start at 0.</span></span>

<span data-ttu-id="ba69f-120">Можно также получить доступ к элементам массива, используя нотацию срез, который позволяет указать поддиапазон массива.</span><span class="sxs-lookup"><span data-stu-id="ba69f-120">You can also access array elements by using slice notation, which enables you to specify a subrange of the array.</span></span> <span data-ttu-id="ba69f-121">В приведенных примерах используется нотация среза.</span><span class="sxs-lookup"><span data-stu-id="ba69f-121">Examples of slice notation follow.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet51.fs)]

<span data-ttu-id="ba69f-122">При использовании нотации slice создается новая копия массива.</span><span class="sxs-lookup"><span data-stu-id="ba69f-122">When slice notation is used, a new copy of the array is created.</span></span>


## <a name="array-types-and-modules"></a><span data-ttu-id="ba69f-123">Типы массивов и модули</span><span class="sxs-lookup"><span data-stu-id="ba69f-123">Array Types and Modules</span></span>
<span data-ttu-id="ba69f-124">Тип всех массивов F # — тип .NET Framework <xref:System.Array?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="ba69f-124">The type of all F# arrays is the .NET Framework type <xref:System.Array?displayProperty=nameWithType>.</span></span> <span data-ttu-id="ba69f-125">Таким образом, массивы F # поддерживают все функциональные возможности, доступные в <xref:System.Array?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="ba69f-125">Therefore, F# arrays support all the functionality available in <xref:System.Array?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="ba69f-126">Модуль библиотеки [ `Microsoft.FSharp.Collections.Array` ](https://msdn.microsoft.com/library/0cda8040-9396-40dd-8dcd-cf48542165a1) поддерживает операции над одномерные массивы.</span><span class="sxs-lookup"><span data-stu-id="ba69f-126">The library module [`Microsoft.FSharp.Collections.Array`](https://msdn.microsoft.com/library/0cda8040-9396-40dd-8dcd-cf48542165a1) supports operations on one-dimensional arrays.</span></span> <span data-ttu-id="ba69f-127">Модули `Array2D`, `Array3D`, и `Array4D` содержат функции, поддерживающие операции над массивами двух, трех и четырех измерений соответственно.</span><span class="sxs-lookup"><span data-stu-id="ba69f-127">The modules `Array2D`, `Array3D`, and `Array4D` contain functions that support operations on arrays of two, three, and four dimensions, respectively.</span></span> <span data-ttu-id="ba69f-128">Можно создать массивы ранга более 4 с помощью <xref:System.Array?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="ba69f-128">You can create arrays of rank greater than four by using <xref:System.Array?displayProperty=nameWithType>.</span></span>

### <a name="simple-functions"></a><span data-ttu-id="ba69f-129">Простые функции</span><span class="sxs-lookup"><span data-stu-id="ba69f-129">Simple Functions</span></span>
<span data-ttu-id="ba69f-130">[`Array.get`](https://msdn.microsoft.com/library/dd93e85d-7e80-4d76-8de0-b6d45bcf07bc)Возвращает элемент.</span><span class="sxs-lookup"><span data-stu-id="ba69f-130">[`Array.get`](https://msdn.microsoft.com/library/dd93e85d-7e80-4d76-8de0-b6d45bcf07bc) gets an element.</span></span> <span data-ttu-id="ba69f-131">[`Array.length`](https://msdn.microsoft.com/library/0d775b6a-4a8f-4bd1-83e5-843b3251725f)предоставляет длину массива.</span><span class="sxs-lookup"><span data-stu-id="ba69f-131">[`Array.length`](https://msdn.microsoft.com/library/0d775b6a-4a8f-4bd1-83e5-843b3251725f) gives the length of an array.</span></span> <span data-ttu-id="ba69f-132">[`Array.set`](https://msdn.microsoft.com/library/847edc0d-4dc5-4a39-98c7-d4320c60e790)Задает элемент с указанным значением.</span><span class="sxs-lookup"><span data-stu-id="ba69f-132">[`Array.set`](https://msdn.microsoft.com/library/847edc0d-4dc5-4a39-98c7-d4320c60e790) sets an element to a specified value.</span></span> <span data-ttu-id="ba69f-133">В следующем примере кода показано использование этих функций.</span><span class="sxs-lookup"><span data-stu-id="ba69f-133">The following code example illustrates the use of these functions.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet9.fs)]

<span data-ttu-id="ba69f-134">Выходные данные выглядят следующим образом.</span><span class="sxs-lookup"><span data-stu-id="ba69f-134">The output is as follows.</span></span>

```
0 1 2 3 4 5 6 7 8 9
```

### <a name="functions-that-create-arrays"></a><span data-ttu-id="ba69f-135">Функции, создающие массивы</span><span class="sxs-lookup"><span data-stu-id="ba69f-135">Functions That Create Arrays</span></span>

<span data-ttu-id="ba69f-136">Несколько функций создают массивы, не требуя существующего массива.</span><span class="sxs-lookup"><span data-stu-id="ba69f-136">Several functions create arrays without requiring an existing array.</span></span> <span data-ttu-id="ba69f-137">[`Array.empty`](https://msdn.microsoft.com/library/c3694b92-1c16-4c54-9bf2-fe398fadce32)Создает новый массив, который не содержит какие-либо элементы.</span><span class="sxs-lookup"><span data-stu-id="ba69f-137">[`Array.empty`](https://msdn.microsoft.com/library/c3694b92-1c16-4c54-9bf2-fe398fadce32) creates a new array that does not contain any elements.</span></span> <span data-ttu-id="ba69f-138">[`Array.create`](https://msdn.microsoft.com/library/e848c8d6-1142-4080-9727-8dacc26066be)Создает массив указанного размера и задает для всех элементов указанные значения.</span><span class="sxs-lookup"><span data-stu-id="ba69f-138">[`Array.create`](https://msdn.microsoft.com/library/e848c8d6-1142-4080-9727-8dacc26066be) creates an array of a specified size and sets all the elements to provided values.</span></span> <span data-ttu-id="ba69f-139">[`Array.init`](https://msdn.microsoft.com/library/ee898089-63b0-40aa-910c-5ae7e32f6665)Создает массив заданного измерения и функции для создания элементов.</span><span class="sxs-lookup"><span data-stu-id="ba69f-139">[`Array.init`](https://msdn.microsoft.com/library/ee898089-63b0-40aa-910c-5ae7e32f6665) creates an array, given a dimension and a function to generate the elements.</span></span> <span data-ttu-id="ba69f-140">[`Array.zeroCreate`](https://msdn.microsoft.com/library/fa5b8e7a-1b5b-411c-8622-b58d7a14d3b2)Создает массив, элементы которого присваивается нулевое значение для типа массива.</span><span class="sxs-lookup"><span data-stu-id="ba69f-140">[`Array.zeroCreate`](https://msdn.microsoft.com/library/fa5b8e7a-1b5b-411c-8622-b58d7a14d3b2) creates an array in which all the elements are initialized to the zero value for the array's type.</span></span> <span data-ttu-id="ba69f-141">Следующий код демонстрирует эти функции.</span><span class="sxs-lookup"><span data-stu-id="ba69f-141">The following code demonstrates these functions.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet91.fs)]

<span data-ttu-id="ba69f-142">Выходные данные выглядят следующим образом.</span><span class="sxs-lookup"><span data-stu-id="ba69f-142">The output is as follows.</span></span>

```
Length of empty array: 0
Area of floats set to 5.0: [|5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0|]
Array of squares: [|0; 1; 4; 9; 16; 25; 36; 49; 64; 81|]
```

<span data-ttu-id="ba69f-143">[`Array.copy`](https://msdn.microsoft.com/library/9d0202f1-1ea0-475e-9d66-4f8ccc3c5b5f)Создает новый массив, содержащий элементы, скопированные из существующего массива.</span><span class="sxs-lookup"><span data-stu-id="ba69f-143">[`Array.copy`](https://msdn.microsoft.com/library/9d0202f1-1ea0-475e-9d66-4f8ccc3c5b5f) creates a new array that contains elements that are copied from an existing array.</span></span> <span data-ttu-id="ba69f-144">Обратите внимание, что копия — это неполная копия, это означает, что если тип элемента является типом ссылки, копируется только ссылка, не базовый объект.</span><span class="sxs-lookup"><span data-stu-id="ba69f-144">Note that the copy is a shallow copy, which means that if the element type is a reference type, only the reference is copied, not the underlying object.</span></span> <span data-ttu-id="ba69f-145">Это показано в следующем примере кода.</span><span class="sxs-lookup"><span data-stu-id="ba69f-145">The following code example illustrates this.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet11.fs)]

<span data-ttu-id="ba69f-146">Результат выполнения предыдущего кода выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ba69f-146">The output of the preceding code is as follows:</span></span>

```
[|Test1; Test2; |]
[|; Test2; |]
```

<span data-ttu-id="ba69f-147">Строка `Test1` появляется только в первом массиве, так как операция создания нового элемента перезаписывает ссылку в `firstArray` , но не влияет на исходную ссылку на пустую строку, которая все еще присутствуют в `secondArray`.</span><span class="sxs-lookup"><span data-stu-id="ba69f-147">The string `Test1` appears only in the first array because the operation of creating a new element overwrites the reference in `firstArray` but does not affect the original reference to an empty string that is still present in `secondArray`.</span></span> <span data-ttu-id="ba69f-148">Строка `Test2` появляется в обоих массивов, поскольку `Insert` операции <xref:System.Text.StringBuilder?displayProperty=nameWithType> тип влияет на базовый <xref:System.Text.StringBuilder?displayProperty=nameWithType> объекта, на которую ссылается оба массива.</span><span class="sxs-lookup"><span data-stu-id="ba69f-148">The string `Test2` appears in both arrays because the `Insert` operation on the <xref:System.Text.StringBuilder?displayProperty=nameWithType> type affects the underlying <xref:System.Text.StringBuilder?displayProperty=nameWithType> object, which is referenced in both arrays.</span></span>

<span data-ttu-id="ba69f-149">[`Array.sub`](https://msdn.microsoft.com/library/40fb12ba-41d7-4ef0-b33a-56727deeef9d)Создает новый массив из массива.</span><span class="sxs-lookup"><span data-stu-id="ba69f-149">[`Array.sub`](https://msdn.microsoft.com/library/40fb12ba-41d7-4ef0-b33a-56727deeef9d) generates a new array from a subrange of an array.</span></span> <span data-ttu-id="ba69f-150">Укажите диапазоны, предоставляя начальный индекс и длину.</span><span class="sxs-lookup"><span data-stu-id="ba69f-150">You specify the subrange by providing the starting index and the length.</span></span> <span data-ttu-id="ba69f-151">В следующем коде показано использование функции `Array.sub`.</span><span class="sxs-lookup"><span data-stu-id="ba69f-151">The following code demonstrates the use of `Array.sub`.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet12.fs)]

<span data-ttu-id="ba69f-152">Выходные данные показывают, что подмассив начинается с элемента 5 и содержит 10 элементов.</span><span class="sxs-lookup"><span data-stu-id="ba69f-152">The output shows that the subarray starts at element 5 and contains 10 elements.</span></span>

```
[|5; 6; 7; 8; 9; 10; 11; 12; 13; 14|]
```
<span data-ttu-id="ba69f-153">[`Array.append`](https://msdn.microsoft.com/library/08836310-5036-4474-b9a2-2c73e2293911)Создает новый массив, объединяя два существующих массива.</span><span class="sxs-lookup"><span data-stu-id="ba69f-153">[`Array.append`](https://msdn.microsoft.com/library/08836310-5036-4474-b9a2-2c73e2293911) creates a new array by combining two existing arrays.</span></span>

<span data-ttu-id="ba69f-154">В следующем коде показано **Array.append**.</span><span class="sxs-lookup"><span data-stu-id="ba69f-154">The following code demonstrates **Array.append**.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet13.fs)]

<span data-ttu-id="ba69f-155">Результат выполнения предыдущего кода выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="ba69f-155">The output of the preceding code is as follows.</span></span>

```
[|1; 2; 3; 4; 5; 6|]
```

<span data-ttu-id="ba69f-156">[`Array.choose`](https://msdn.microsoft.com/library/f5c8a5e2-637f-44d4-b35c-be96a6618b09)Выбор элементов в массиве, включаемых в новый массив.</span><span class="sxs-lookup"><span data-stu-id="ba69f-156">[`Array.choose`](https://msdn.microsoft.com/library/f5c8a5e2-637f-44d4-b35c-be96a6618b09) selects elements of an array to include in a new array.</span></span> <span data-ttu-id="ba69f-157">В следующем коде показано `Array.choose`.</span><span class="sxs-lookup"><span data-stu-id="ba69f-157">The following code demonstrates `Array.choose`.</span></span> <span data-ttu-id="ba69f-158">Обратите внимание, что тип элемента массива не совпадает с типом значения, возвращаемого в параметр типа.</span><span class="sxs-lookup"><span data-stu-id="ba69f-158">Note that the element type of the array does not have to match the type of the value returned in the option type.</span></span> <span data-ttu-id="ba69f-159">В этом примере тип элемента — это `int` результат полиномиальной функции, а параметр `elem*elem - 1`, как число с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="ba69f-159">In this example, the element type is `int` and the option is the result of a polynomial function, `elem*elem - 1`, as a floating point number.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet14.fs)]

<span data-ttu-id="ba69f-160">Результат выполнения предыдущего кода выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="ba69f-160">The output of the preceding code is as follows.</span></span>

```
[|3.0; 15.0; 35.0; 63.0; 99.0|]
```

<span data-ttu-id="ba69f-161">[`Array.collect`](https://msdn.microsoft.com/library/c3b60c3b-9455-48c9-bc2b-e88f0434342a)Выполняет указанную функцию к каждому элементу существующего массива и собирает элементы, создаваемые функцией и объединяет их в новый массив.</span><span class="sxs-lookup"><span data-stu-id="ba69f-161">[`Array.collect`](https://msdn.microsoft.com/library/c3b60c3b-9455-48c9-bc2b-e88f0434342a) runs a specified function on each array element of an existing array and then collects the elements generated by the function and combines them into a new array.</span></span> <span data-ttu-id="ba69f-162">В следующем коде показано `Array.collect`.</span><span class="sxs-lookup"><span data-stu-id="ba69f-162">The following code demonstrates `Array.collect`.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet15.fs)]

<span data-ttu-id="ba69f-163">Результат выполнения предыдущего кода выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="ba69f-163">The output of the preceding code is as follows.</span></span>

```
[|0; 1; 0; 1; 2; 3; 4; 5; 0; 1; 2; 3; 4; 5; 6; 7; 8; 9; 10|]
```

<span data-ttu-id="ba69f-164">[`Array.concat`](https://msdn.microsoft.com/library/f7219b79-1ec8-4a25-96b1-edbedb358302)Получает последовательность массивов и объединяет их в одном массиве.</span><span class="sxs-lookup"><span data-stu-id="ba69f-164">[`Array.concat`](https://msdn.microsoft.com/library/f7219b79-1ec8-4a25-96b1-edbedb358302) takes a sequence of arrays and combines them into a single array.</span></span> <span data-ttu-id="ba69f-165">В следующем коде показано `Array.concat`.</span><span class="sxs-lookup"><span data-stu-id="ba69f-165">The following code demonstrates `Array.concat`.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet16.fs)]

<span data-ttu-id="ba69f-166">Результат выполнения предыдущего кода выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="ba69f-166">The output of the preceding code is as follows.</span></span>

```
[|(1, 1, 1); (1, 2, 2); (1, 3, 3); (2, 1, 2); (2, 2, 4); (2, 3, 6); (3, 1, 3);
(3, 2, 6); (3, 3, 9)|]
```

<span data-ttu-id="ba69f-167">[`Array.filter`](https://msdn.microsoft.com/library/b885b214-47fc-4639-9664-b8c183a39ede)использует функцию логическое условие и создает новый массив, содержащий только те элементы входного массива, для которого условие имеет значение true.</span><span class="sxs-lookup"><span data-stu-id="ba69f-167">[`Array.filter`](https://msdn.microsoft.com/library/b885b214-47fc-4639-9664-b8c183a39ede) takes a Boolean condition function and generates a new array that contains only those elements from the input array for which the condition is true.</span></span> <span data-ttu-id="ba69f-168">В следующем коде показано `Array.filter`.</span><span class="sxs-lookup"><span data-stu-id="ba69f-168">The following code demonstrates `Array.filter`.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet17.fs)]

<span data-ttu-id="ba69f-169">Результат выполнения предыдущего кода выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="ba69f-169">The output of the preceding code is as follows.</span></span>

```
[|2; 4; 6; 8; 10|]
```

<span data-ttu-id="ba69f-170">[`Array.rev`](https://msdn.microsoft.com/library/1bbf822c-763b-4794-af21-97d2e48ef709)Создает новый массив, изменяя порядок существующего массива.</span><span class="sxs-lookup"><span data-stu-id="ba69f-170">[`Array.rev`](https://msdn.microsoft.com/library/1bbf822c-763b-4794-af21-97d2e48ef709) generates a new array by reversing the order of an existing array.</span></span> <span data-ttu-id="ba69f-171">В следующем коде показано `Array.rev`.</span><span class="sxs-lookup"><span data-stu-id="ba69f-171">The following code demonstrates `Array.rev`.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet18.fs)]  

<span data-ttu-id="ba69f-172">Результат выполнения предыдущего кода выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="ba69f-172">The output of the preceding code is as follows.</span></span>

```
"Hello world!"
```

<span data-ttu-id="ba69f-173">Можно легко объединять функции в модуле массива, которые преобразуют массивов с помощью оператора конвейера (`|>`), как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="ba69f-173">You can easily combine functions in the array module that transform arrays by using the pipeline operator (`|>`), as shown in the following example.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet19.fs)]

<span data-ttu-id="ba69f-174">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ba69f-174">The output is</span></span>

```
[|100; 36; 16; 4|]
```

### <a name="multidimensional-arrays"></a><span data-ttu-id="ba69f-175">Многомерные массивы</span><span class="sxs-lookup"><span data-stu-id="ba69f-175">Multidimensional Arrays</span></span>

<span data-ttu-id="ba69f-176">Многомерные массивы могут создаваться, но есть синтаксис многомерных литерала массива.</span><span class="sxs-lookup"><span data-stu-id="ba69f-176">A multidimensional array can be created, but there is no syntax for writing a multidimensional array literal.</span></span> <span data-ttu-id="ba69f-177">Используйте оператор [ `array2D` ](https://msdn.microsoft.com/library/1d52503d-2990-49fc-8fd3-6b0e508aa236) для создания массива из последовательности последовательностей элементов массива.</span><span class="sxs-lookup"><span data-stu-id="ba69f-177">Use the operator [`array2D`](https://msdn.microsoft.com/library/1d52503d-2990-49fc-8fd3-6b0e508aa236) to create an array from a sequence of sequences of array elements.</span></span> <span data-ttu-id="ba69f-178">Последовательности могут быть литералами массивов или списков.</span><span class="sxs-lookup"><span data-stu-id="ba69f-178">The sequences can be array or list literals.</span></span> <span data-ttu-id="ba69f-179">Например следующий код создает двумерный массив.</span><span class="sxs-lookup"><span data-stu-id="ba69f-179">For example, the following code creates a two-dimensional array.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet20.fs)]

<span data-ttu-id="ba69f-180">Можно также использовать функцию [ `Array2D.init` ](https://msdn.microsoft.com/library/9de07e95-bc21-4927-b5b4-08fdec882c7b) для инициализации массива двух измерений и аналогичные функции доступны для массивов, трех и четырех измерений.</span><span class="sxs-lookup"><span data-stu-id="ba69f-180">You can also use the function [`Array2D.init`](https://msdn.microsoft.com/library/9de07e95-bc21-4927-b5b4-08fdec882c7b) to initialize arrays of two dimensions, and similar functions are available for arrays of three and four dimensions.</span></span> <span data-ttu-id="ba69f-181">Эти функции принимают функцию, которая используется для создания элементов.</span><span class="sxs-lookup"><span data-stu-id="ba69f-181">These functions take a function that is used to create the elements.</span></span> <span data-ttu-id="ba69f-182">Чтобы создать двумерный массив, содержащий элементы, задать начальное значение вместо указания функции, используйте [ `Array2D.create` ](https://msdn.microsoft.com/library/36c9d980-b241-4a20-bc64-bcfa0205d804) функции, которая доступна для массивов до четырех измерений.</span><span class="sxs-lookup"><span data-stu-id="ba69f-182">To create a two-dimensional array that contains elements set to an initial value instead of specifying a function, use the [`Array2D.create`](https://msdn.microsoft.com/library/36c9d980-b241-4a20-bc64-bcfa0205d804) function, which is also available for arrays up to four dimensions.</span></span> <span data-ttu-id="ba69f-183">В следующем примере кода показано создание массива массивов, которые содержат необходимых элементов, а затем использует `Array2D.init` для создания нужного двумерного массива.</span><span class="sxs-lookup"><span data-stu-id="ba69f-183">The following code example first shows how to create an array of arrays that contain the desired elements, and then uses `Array2D.init` to generate the desired two-dimensional array.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet21.fs)]

<span data-ttu-id="ba69f-184">Массив, индексирования и создания срезов синтаксиса поддерживается для массивов не более 4 ранга.</span><span class="sxs-lookup"><span data-stu-id="ba69f-184">Array indexing and slicing syntax is supported for arrays up to rank 4.</span></span> <span data-ttu-id="ba69f-185">При указании индекса в нескольких измерениях, ставя несколько запятых для разделения индексов, как показано в следующем примере кода.</span><span class="sxs-lookup"><span data-stu-id="ba69f-185">When you specify an index in multiple dimensions, you use commas to separate the indexes, as illustrated in the following code example.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet22.fs)]
    
<span data-ttu-id="ba69f-186">Тип двумерный массив записывается как `<type>[,]` (например, `int[,]`, `double[,]`), и тип трехмерного массива записывается как `<type>[,,]`, и так далее для многомерных массивов.</span><span class="sxs-lookup"><span data-stu-id="ba69f-186">The type of a two-dimensional array is written out as `<type>[,]` (for example, `int[,]`, `double[,]`), and the type of a three-dimensional array is written as `<type>[,,]`, and so on for arrays of higher dimensions.</span></span>

<span data-ttu-id="ba69f-187">Для многомерных массивов также доступен только подмножество функций, доступных для одномерных массивов.</span><span class="sxs-lookup"><span data-stu-id="ba69f-187">Only a subset of the functions available for one-dimensional arrays is also available for multidimensional arrays.</span></span> <span data-ttu-id="ba69f-188">Дополнительные сведения см. в разделе [ `Collections.Array Module` ](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array-module-%5bfsharp%5d), [ `Collections.Array2D Module` ](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array2d-module-%5bfsharp%5d), [ `Collections.Array3D Module` ](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array3d-module-%5bfsharp%5d), и [ `Collections.Array4D Module` ](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array4d-module-%5bfsharp%5d).</span><span class="sxs-lookup"><span data-stu-id="ba69f-188">For more information, see [`Collections.Array Module`](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array-module-%5bfsharp%5d), [`Collections.Array2D Module`](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array2d-module-%5bfsharp%5d), [`Collections.Array3D Module`](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array3d-module-%5bfsharp%5d), and [`Collections.Array4D Module`](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array4d-module-%5bfsharp%5d).</span></span>

### <a name="array-slicing-and-multidimensional-arrays"></a><span data-ttu-id="ba69f-189">Создание срезов массива и многомерные массивы</span><span class="sxs-lookup"><span data-stu-id="ba69f-189">Array Slicing and Multidimensional Arrays</span></span>

<span data-ttu-id="ba69f-190">В двумерный массив (матрица), можно извлекать вложенные матрицы, указав диапазоны и с помощью подстановочного знака (`*`) символ для указания целых строк или столбцов.</span><span class="sxs-lookup"><span data-stu-id="ba69f-190">In a two-dimensional array (a matrix), you can extract a sub-matrix by specifying ranges and using a wildcard (`*`) character to specify whole rows or columns.</span></span>

```fsharp
/ Get rows 1 to N from an NxM matrix (returns a matrix):
matrix.[1.., *]

// Get rows 1 to 3 from a matrix (returns a matrix):
matrix.[1..3, *]

// Get columns 1 to 3 from a matrix (returns a matrix):
matrix.[*, 1..3]

// Get a 3x3 submatrix:
matrix.[1..3, 1..3]
```

<span data-ttu-id="ba69f-191">Начиная с версии 3.1 языка F # многомерного массива можно разбить на подмассивов измерения же или более ранней.</span><span class="sxs-lookup"><span data-stu-id="ba69f-191">As of F# 3.1, you can decompose a multidimensional array into subarrays of the same or lower dimension.</span></span> <span data-ttu-id="ba69f-192">Например можно получить вектор из матрицы, указав одну строку или столбец.</span><span class="sxs-lookup"><span data-stu-id="ba69f-192">For example, you can obtain a vector from a matrix by specifying a single row or column.</span></span>

```fsharp
// Get row 3 from a matrix as a vector:
matrix.[3, *]

// Get column 3 from a matrix as a vector:
matrix.[*, 3]
```

<span data-ttu-id="ba69f-193">Эту функцию можно использовать синтаксис для типов, которые реализуют операторы для доступа к элементу и перегруженные Фрагментирование `GetSlice` методы.</span><span class="sxs-lookup"><span data-stu-id="ba69f-193">You can use this slicing syntax for types that implement the element access operators and overloaded `GetSlice` methods.</span></span> <span data-ttu-id="ba69f-194">Например, следующий код создает тип матрицы, который инкапсулирует двухмерного массива F #, реализует свойство элемента для обеспечения поддержки индексация массива и реализует три версии `GetSlice`.</span><span class="sxs-lookup"><span data-stu-id="ba69f-194">For example, the following code creates a Matrix type that wraps the F# 2D array, implements an Item property to provide support for array indexing, and implements three versions of `GetSlice`.</span></span> <span data-ttu-id="ba69f-195">Если этот код можно использовать как шаблон матрицы типов, можно использовать все среза операции, которые описаны в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="ba69f-195">If you can use this code as a template for your matrix types, you can use all the slicing operations that this section describes.</span></span>

```fsharp
type Matrix<'T>(N: int, M: int) =
    let internalArray = Array2D.zeroCreate<'T> N M

    member this.Item
        with get(a: int, b: int) = internalArray.[a, b]
        and set(a: int, b: int) (value:'T) = internalArray.[a, b] <- value

    member this.GetSlice(rowStart: int option, rowFinish : int option, colStart: int option, colFinish : int option) =
        let rowStart = 
            match rowStart with
            | Some(v) -> v
            | None -> 0
        let rowFinish =
            match rowFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(0) - 1
        let colStart = 
            match colStart with
            | Some(v) -> v
            | None -> 0
        let colFinish = 
            match colFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(1) - 1
        internalArray.[rowStart..rowFinish, colStart..colFinish]

    member this.GetSlice(row: int, colStart: int option, colFinish: int option) =
        let colStart = 
            match colStart with
            | Some(v) -> v
            | None -> 0
        let colFinish = 
            match colFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(1) - 1
        internalArray.[row, colStart..colFinish]

    member this.GetSlice(rowStart: int option, rowFinish: int option, col: int) =
        let rowStart = 
            match rowStart with
            | Some(v) -> v
            | None -> 0
        let rowFinish = 
            match rowFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(0) - 1
        internalArray.[rowStart..rowFinish, col]

module test =
    let generateTestMatrix x y =
        let matrix = new Matrix<float>(3, 3)
        for i in 0..2 do
            for j in 0..2 do
                matrix.[i, j] <- float(i) * x - float(j) * y
        matrix

    let test1 = generateTestMatrix 2.3 1.1
    let submatrix = test1.[0..1, 0..1]
    printfn "%A" submatrix

    let firstRow = test1.[0,*]
    let secondRow = test1.[1,*]
    let firstCol = test1.[*,0]
    printfn "%A" firstCol
```

### <a name="boolean-functions-on-arrays"></a><span data-ttu-id="ba69f-196">Логические функции для массивов</span><span class="sxs-lookup"><span data-stu-id="ba69f-196">Boolean Functions on Arrays</span></span>

<span data-ttu-id="ba69f-197">Функции [ `Array.exists` ](https://msdn.microsoft.com/library/8e47ad6c-c065-4876-8cb4-ec960ec3e5c9) и [ `Array.exists2` ](https://msdn.microsoft.com/library/2e384a6a-f99d-4e23-b677-250ffbc1dd8e) проверки элементов в одной или двух массивов, соответственно.</span><span class="sxs-lookup"><span data-stu-id="ba69f-197">The functions [`Array.exists`](https://msdn.microsoft.com/library/8e47ad6c-c065-4876-8cb4-ec960ec3e5c9) and [`Array.exists2`](https://msdn.microsoft.com/library/2e384a6a-f99d-4e23-b677-250ffbc1dd8e) test elements in either one or two arrays, respectively.</span></span> <span data-ttu-id="ba69f-198">Эти функции принимают функцию проверки и возвращают `true` при наличии элемента (или `Array.exists2`), удовлетворяющий условию.</span><span class="sxs-lookup"><span data-stu-id="ba69f-198">These functions take a test function and return `true` if there is an element (or element pair for `Array.exists2`) that satisfies the condition.</span></span>

<span data-ttu-id="ba69f-199">В следующем коде показано использование `Array.exists` и `Array.exists2`.</span><span class="sxs-lookup"><span data-stu-id="ba69f-199">The following code demonstrates the use of `Array.exists` and `Array.exists2`.</span></span> <span data-ttu-id="ba69f-200">В этих примерах новые функции создаются путем использования только одного из аргументов, в этих случаях аргумент функции.</span><span class="sxs-lookup"><span data-stu-id="ba69f-200">In these examples, new functions are created by applying only one of the arguments, in these cases, the function argument.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet23.fs)]

<span data-ttu-id="ba69f-201">Результат выполнения предыдущего кода выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="ba69f-201">The output of the preceding code is as follows.</span></span>

```
true
false
false
true
```

<span data-ttu-id="ba69f-202">Аналогичным образом, функция [ `Array.forall` ](https://msdn.microsoft.com/library/d88f2cd0-fa7f-45cf-ac15-31eae9086cc4) проверяет массива, чтобы определить, удовлетворяет ли каждый элемент является логическое условие.</span><span class="sxs-lookup"><span data-stu-id="ba69f-202">Similarly, the function [`Array.forall`](https://msdn.microsoft.com/library/d88f2cd0-fa7f-45cf-ac15-31eae9086cc4) tests an array to determine whether every element satisfies a Boolean condition.</span></span> <span data-ttu-id="ba69f-203">Значение варианта [ `Array.forall2` ](https://msdn.microsoft.com/library/c68f61a1-030c-4024-b705-c4768b6c96b9) делает то же самое с помощью логической функции, принимающей элементы двух массивов одинаковой длины.</span><span class="sxs-lookup"><span data-stu-id="ba69f-203">The variation [`Array.forall2`](https://msdn.microsoft.com/library/c68f61a1-030c-4024-b705-c4768b6c96b9) does the same thing by using a Boolean function that involves elements of two arrays of equal length.</span></span> <span data-ttu-id="ba69f-204">Следующий код иллюстрирует использование этих функций.</span><span class="sxs-lookup"><span data-stu-id="ba69f-204">The following code illustrates the use of these functions.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet24.fs)]

<span data-ttu-id="ba69f-205">Результат выполнения этих примеров выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="ba69f-205">The output for these examples is as follows.</span></span>

```
false
true
true
false
```

### <a name="searching-arrays"></a><span data-ttu-id="ba69f-206">Поиск в массивах</span><span class="sxs-lookup"><span data-stu-id="ba69f-206">Searching Arrays</span></span>

<span data-ttu-id="ba69f-207">[`Array.find`](https://msdn.microsoft.com/library/db6d920a-de19-4520-85a4-d83de77c1b33)принимает логическую функцию и возвращает первый элемент, для которых функция возвращает `true`, или вызывает <xref:System.Collections.Generic.KeyNotFoundException?displayProperty=nameWithType> Если найден ни один элемент, удовлетворяющий условию.</span><span class="sxs-lookup"><span data-stu-id="ba69f-207">[`Array.find`](https://msdn.microsoft.com/library/db6d920a-de19-4520-85a4-d83de77c1b33) takes a Boolean function and returns the first element for which the function returns `true`, or raises a <xref:System.Collections.Generic.KeyNotFoundException?displayProperty=nameWithType> if no element that satisfies the condition is found.</span></span> <span data-ttu-id="ba69f-208">[`Array.findIndex`](https://msdn.microsoft.com/library/5ae3a8f9-7b8f-44ea-a740-d5700f4d899f)Подобно `Array.find`, за исключением того, что она возвращает индекс элемента, а не сам элемент.</span><span class="sxs-lookup"><span data-stu-id="ba69f-208">[`Array.findIndex`](https://msdn.microsoft.com/library/5ae3a8f9-7b8f-44ea-a740-d5700f4d899f) is like `Array.find`, except that it returns the index of the element instead of the element itself.</span></span>

<span data-ttu-id="ba69f-209">В следующем коде используется `Array.find` и `Array.findIndex` для поиска числа, которое одновременно является точным квадратом и точным кубом.</span><span class="sxs-lookup"><span data-stu-id="ba69f-209">The following code uses `Array.find` and `Array.findIndex` to locate a number that is both a perfect square and perfect cube.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet25.fs)]

<span data-ttu-id="ba69f-210">Выходные данные выглядят следующим образом.</span><span class="sxs-lookup"><span data-stu-id="ba69f-210">The output is as follows.</span></span>

```
The first element that is both a square and a cube is 64 and its index is 62.
```

<span data-ttu-id="ba69f-211">[`Array.tryFind`](https://msdn.microsoft.com/library/7bd65f6c-df77-454c-ac3a-6f7baecec9d9)Подобно `Array.find`, за исключением того, что ее результат имеет тип параметра и возвращает `None` , если элемент не найден.</span><span class="sxs-lookup"><span data-stu-id="ba69f-211">[`Array.tryFind`](https://msdn.microsoft.com/library/7bd65f6c-df77-454c-ac3a-6f7baecec9d9) is like `Array.find`, except that its result is an option type, and it returns `None` if no element is found.</span></span> <span data-ttu-id="ba69f-212">`Array.tryFind`следует использовать вместо `Array.find` Если вы не знаете ли соответствующий элемент в массиве.</span><span class="sxs-lookup"><span data-stu-id="ba69f-212">`Array.tryFind` should be used instead of `Array.find` when you do not know whether a matching element is in the array.</span></span> <span data-ttu-id="ba69f-213">Аналогичным образом [ `Array.tryFindIndex` ](https://msdn.microsoft.com/library/da82f7fe-95e9-4fd5-a924-cd3c9d10618a) подобно [ `Array.findIndex` ](https://msdn.microsoft.com/library/5ae3a8f9-7b8f-44ea-a740-d5700f4d899f) за исключением того, что тип параметра является возвращаемым значением.</span><span class="sxs-lookup"><span data-stu-id="ba69f-213">Similarly, [`Array.tryFindIndex`](https://msdn.microsoft.com/library/da82f7fe-95e9-4fd5-a924-cd3c9d10618a) is like [`Array.findIndex`](https://msdn.microsoft.com/library/5ae3a8f9-7b8f-44ea-a740-d5700f4d899f) except that the option type is the return value.</span></span> <span data-ttu-id="ba69f-214">Если элемент не найден, параметр — `None`.</span><span class="sxs-lookup"><span data-stu-id="ba69f-214">If no element is found, the option is `None`.</span></span>

<span data-ttu-id="ba69f-215">В следующем коде показано использование функции `Array.tryFind`.</span><span class="sxs-lookup"><span data-stu-id="ba69f-215">The following code demonstrates the use of `Array.tryFind`.</span></span> <span data-ttu-id="ba69f-216">Этот код зависит от предыдущего кода.</span><span class="sxs-lookup"><span data-stu-id="ba69f-216">This code depends on the previous code.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet26.fs)]

<span data-ttu-id="ba69f-217">Выходные данные выглядят следующим образом.</span><span class="sxs-lookup"><span data-stu-id="ba69f-217">The output is as follows.</span></span>

```
Found an element: 1
Found an element: 729
```

<span data-ttu-id="ba69f-218">Используйте [ `Array.tryPick` ](https://msdn.microsoft.com/library/72d45f85-037b-43a9-97fd-17239f72713e) при необходимости преобразования элемента его.</span><span class="sxs-lookup"><span data-stu-id="ba69f-218">Use [`Array.tryPick`](https://msdn.microsoft.com/library/72d45f85-037b-43a9-97fd-17239f72713e) when you need to transform an element in addition to finding it.</span></span> <span data-ttu-id="ba69f-219">Результатом является первым элементом, для которого функция возвращает преобразованный элемент как значение параметра или `None` , если элемент не найден.</span><span class="sxs-lookup"><span data-stu-id="ba69f-219">The result is the first element for which the function returns the transformed element as an option value, or `None` if no such element is found.</span></span>

<span data-ttu-id="ba69f-220">В следующем коде показано использование `Array.tryPick`.</span><span class="sxs-lookup"><span data-stu-id="ba69f-220">The following code shows the use of `Array.tryPick`.</span></span> <span data-ttu-id="ba69f-221">В этом случае вместо лямбда-выражение для упрощения кода определяются несколько локальных вспомогательных функций.</span><span class="sxs-lookup"><span data-stu-id="ba69f-221">In this case, instead of a lambda expression, several local helper functions are defined to simplify the code.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet27.fs)]

<span data-ttu-id="ba69f-222">Выходные данные выглядят следующим образом.</span><span class="sxs-lookup"><span data-stu-id="ba69f-222">The output is as follows.</span></span>

```
Found an element 1 with square root 1 and cube root 1.
Found an element 64 with square root 8 and cube root 4.
Found an element 729 with square root 27 and cube root 9.
Found an element 4096 with square root 64 and cube root 16.
```

### <a name="performing-computations-on-arrays"></a><span data-ttu-id="ba69f-223">Вычисления с массивами</span><span class="sxs-lookup"><span data-stu-id="ba69f-223">Performing Computations on Arrays</span></span>

<span data-ttu-id="ba69f-224">[ `Array.average` ](https://msdn.microsoft.com/library/7029f2b9-91ea-41cb-be1b-466a5a0db20e) Функция возвращает среднее значение каждого элемента в массиве.</span><span class="sxs-lookup"><span data-stu-id="ba69f-224">The [`Array.average`](https://msdn.microsoft.com/library/7029f2b9-91ea-41cb-be1b-466a5a0db20e) function returns the average of each element in an array.</span></span> <span data-ttu-id="ba69f-225">Ограничена типами элементов, поддерживающими точное деление на целое число, которое включает типы с плавающей запятой, но не целочисленные типы.</span><span class="sxs-lookup"><span data-stu-id="ba69f-225">It is limited to element types that support exact division by an integer, which includes floating point types but not integral types.</span></span> <span data-ttu-id="ba69f-226">[ `Array.averageBy` ](https://msdn.microsoft.com/library/e9d64609-06a3-48f0-bc07-226ab0f85c54) Функция возвращает среднее значение результатов вызова функции для каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="ba69f-226">The [`Array.averageBy`](https://msdn.microsoft.com/library/e9d64609-06a3-48f0-bc07-226ab0f85c54) function returns the average of the results of calling a function on each element.</span></span> <span data-ttu-id="ba69f-227">Для массива целочисленный тип, можно использовать `Array.averageBy` и с помощью функции преобразования каждого элемента в число с плавающей запятой для вычисления.</span><span class="sxs-lookup"><span data-stu-id="ba69f-227">For an array of integral type, you can use `Array.averageBy` and have the function convert each element to a floating point type for the computation.</span></span>

<span data-ttu-id="ba69f-228">Используйте [ `Array.max` ](https://msdn.microsoft.com/library/f03fbda0-fce6-40e2-a85d-79c9d81f710b) или [ `Array.min` ](https://msdn.microsoft.com/library/d6b3da5f-bac0-4355-9846-4b72d95bc3fd) получить максимальный и минимальный элемент, если его поддерживает тип элемента.</span><span class="sxs-lookup"><span data-stu-id="ba69f-228">Use [`Array.max`](https://msdn.microsoft.com/library/f03fbda0-fce6-40e2-a85d-79c9d81f710b) or [`Array.min`](https://msdn.microsoft.com/library/d6b3da5f-bac0-4355-9846-4b72d95bc3fd) to get the maximum or minimum element, if the element type supports it.</span></span> <span data-ttu-id="ba69f-229">Аналогичным образом [ `Array.maxBy` ](https://msdn.microsoft.com/library/18dbe7c5-482e-4766-8e01-12a76f847045) и [ `Array.minBy` ](https://msdn.microsoft.com/library/24091583-be78-4cc9-9fab-de6d7506af4f) позволяют функции сначала, например для преобразования в тип, поддерживающий сравнение.</span><span class="sxs-lookup"><span data-stu-id="ba69f-229">Similarly, [`Array.maxBy`](https://msdn.microsoft.com/library/18dbe7c5-482e-4766-8e01-12a76f847045) and [`Array.minBy`](https://msdn.microsoft.com/library/24091583-be78-4cc9-9fab-de6d7506af4f) allow a function to be executed first, perhaps to transform to a type that supports comparison.</span></span>

<span data-ttu-id="ba69f-230">[`Array.sum`](https://msdn.microsoft.com/library/4ffdb8c8-cd94-4b0b-9e5c-a7c9c17963c2)Добавляет элементы массива, и [ `Array.sumBy` ](https://msdn.microsoft.com/library/41698ba6-1adc-4169-8cc5-7a0e3f8de56b) вызывает функцию для каждого элемента и складывает результаты.</span><span class="sxs-lookup"><span data-stu-id="ba69f-230">[`Array.sum`](https://msdn.microsoft.com/library/4ffdb8c8-cd94-4b0b-9e5c-a7c9c17963c2) adds the elements of an array, and [`Array.sumBy`](https://msdn.microsoft.com/library/41698ba6-1adc-4169-8cc5-7a0e3f8de56b) calls a function on each element and adds the results together.</span></span>

<span data-ttu-id="ba69f-231">Чтобы выполнить функцию для каждого элемента массива без сохранения возвращаемого значения, используйте [ `Array.iter` ](https://msdn.microsoft.com/library/94eba0f1-ecd7-459f-b89f-ed2a2923e516).</span><span class="sxs-lookup"><span data-stu-id="ba69f-231">To execute a function on each element in an array without storing the return values, use [`Array.iter`](https://msdn.microsoft.com/library/94eba0f1-ecd7-459f-b89f-ed2a2923e516).</span></span> <span data-ttu-id="ba69f-232">Функция двумя массивами одинаковой длины, используйте [ `Array.iter2` ](https://msdn.microsoft.com/library/018aa9b9-f186-4142-be8a-a62462794fdc).</span><span class="sxs-lookup"><span data-stu-id="ba69f-232">For a function involving two arrays of equal length, use [`Array.iter2`](https://msdn.microsoft.com/library/018aa9b9-f186-4142-be8a-a62462794fdc).</span></span> <span data-ttu-id="ba69f-233">Если необходимо сохранить массив результатов функции использовать [ `Array.map` ](https://msdn.microsoft.com/library/38cbe824-0480-47be-85fd-df3afdd97a45) или [ `Array.map2` ](https://msdn.microsoft.com/library/bb7aafe8-4a1f-45b9-92fc-1af9eafbea5c), работающему над двумя массивами одновременно.</span><span class="sxs-lookup"><span data-stu-id="ba69f-233">If you also need to keep an array of the results of the function, use [`Array.map`](https://msdn.microsoft.com/library/38cbe824-0480-47be-85fd-df3afdd97a45) or [`Array.map2`](https://msdn.microsoft.com/library/bb7aafe8-4a1f-45b9-92fc-1af9eafbea5c), which operates on two arrays at a time.</span></span>

<span data-ttu-id="ba69f-234">Варианты [ `Array.iteri` ](https://msdn.microsoft.com/library/8bbe2ed4-ada7-4906-ac3e-cb09f9db6486) и [ `Array.iteri2` ](https://msdn.microsoft.com/library/c041b91f-6080-45b7-867b-2ed983a90405) разрешает индекс элемента, который участвует в вычислении, то же самое справедливо для [ `Array.mapi` ](https://msdn.microsoft.com/library/f7e45994-b0a1-49e6-8fb5-5641cea8fde4) и [ `Array.mapi2` ](https://msdn.microsoft.com/library/5edb33d2-47da-44e1-9290-40c00c47d5b0).</span><span class="sxs-lookup"><span data-stu-id="ba69f-234">The variations [`Array.iteri`](https://msdn.microsoft.com/library/8bbe2ed4-ada7-4906-ac3e-cb09f9db6486) and [`Array.iteri2`](https://msdn.microsoft.com/library/c041b91f-6080-45b7-867b-2ed983a90405) allow the index of the element to be involved in the computation; the same is true for [`Array.mapi`](https://msdn.microsoft.com/library/f7e45994-b0a1-49e6-8fb5-5641cea8fde4) and [`Array.mapi2`](https://msdn.microsoft.com/library/5edb33d2-47da-44e1-9290-40c00c47d5b0).</span></span>

<span data-ttu-id="ba69f-235">Функции [ `Array.fold` ](https://msdn.microsoft.com/library/5ed9dd3b-3694-4567-94d0-fd9a24474e09), [ `Array.foldBack` ](https://msdn.microsoft.com/library/1121a453-dead-4711-a0ca-cc147752989c), [ `Array.reduce` ](https://msdn.microsoft.com/library/fd62a985-89fe-4f49-a9d4-0c808ac6749d), [ `Array.reduceBack` ](https://msdn.microsoft.com/library/4fdd4cbe-2238-4c5c-b286-597a7e9036f9), [ `Array.scan` ](https://msdn.microsoft.com/library/f6893608-9146-450d-9ebb-a0016803fbb0), и [ `Array.scanBack` ](https://msdn.microsoft.com/library/7610f406-7a5c-41db-a0ca-8e2a2a4826ad) выполнение алгоритмы, которые включают все элементы массива.</span><span class="sxs-lookup"><span data-stu-id="ba69f-235">The functions [`Array.fold`](https://msdn.microsoft.com/library/5ed9dd3b-3694-4567-94d0-fd9a24474e09), [`Array.foldBack`](https://msdn.microsoft.com/library/1121a453-dead-4711-a0ca-cc147752989c), [`Array.reduce`](https://msdn.microsoft.com/library/fd62a985-89fe-4f49-a9d4-0c808ac6749d), [`Array.reduceBack`](https://msdn.microsoft.com/library/4fdd4cbe-2238-4c5c-b286-597a7e9036f9), [`Array.scan`](https://msdn.microsoft.com/library/f6893608-9146-450d-9ebb-a0016803fbb0), and [`Array.scanBack`](https://msdn.microsoft.com/library/7610f406-7a5c-41db-a0ca-8e2a2a4826ad) execute algorithms that involve all the elements of an array.</span></span> <span data-ttu-id="ba69f-236">Аналогичным образом, варианты [ `Array.fold2` ](https://msdn.microsoft.com/library/5c845087-d041-476e-8cc4-53ae6849ef79) и [ `Array.foldBack2` ](https://msdn.microsoft.com/library/aa51b405-df20-4c51-9998-a6530f7db862) выполнения вычислений над двумя массивами.</span><span class="sxs-lookup"><span data-stu-id="ba69f-236">Similarly, the variations [`Array.fold2`](https://msdn.microsoft.com/library/5c845087-d041-476e-8cc4-53ae6849ef79) and [`Array.foldBack2`](https://msdn.microsoft.com/library/aa51b405-df20-4c51-9998-a6530f7db862) perform computations on two arrays.</span></span>

<span data-ttu-id="ba69f-237">Эти функции для выполнения вычислений соответствуют функциям с тем же именем в [модуль списка](https://msdn.microsoft.com/library/a2264ba3-2d45-40dd-9040-4f7aa2ad9788).</span><span class="sxs-lookup"><span data-stu-id="ba69f-237">These functions for performing computations correspond to the functions of the same name in the [List module](https://msdn.microsoft.com/library/a2264ba3-2d45-40dd-9040-4f7aa2ad9788).</span></span> <span data-ttu-id="ba69f-238">Примеры использования см. в разделе [перечислены](lists.md).</span><span class="sxs-lookup"><span data-stu-id="ba69f-238">For usage examples, see [Lists](lists.md).</span></span>

### <a name="modifying-arrays"></a><span data-ttu-id="ba69f-239">Изменение массивов</span><span class="sxs-lookup"><span data-stu-id="ba69f-239">Modifying Arrays</span></span>

<span data-ttu-id="ba69f-240">[`Array.set`](https://msdn.microsoft.com/library/847edc0d-4dc5-4a39-98c7-d4320c60e790)Задает элемент с указанным значением.</span><span class="sxs-lookup"><span data-stu-id="ba69f-240">[`Array.set`](https://msdn.microsoft.com/library/847edc0d-4dc5-4a39-98c7-d4320c60e790) sets an element to a specified value.</span></span> <span data-ttu-id="ba69f-241">[`Array.fill`](https://msdn.microsoft.com/library/c83c9886-81d9-44f9-a195-61c7b87f7df2)Задает диапазон элементов в массиве, с указанным значением.</span><span class="sxs-lookup"><span data-stu-id="ba69f-241">[`Array.fill`](https://msdn.microsoft.com/library/c83c9886-81d9-44f9-a195-61c7b87f7df2) sets a range of elements in an array to a specified value.</span></span> <span data-ttu-id="ba69f-242">Ниже приведен пример `Array.fill`.</span><span class="sxs-lookup"><span data-stu-id="ba69f-242">The following code provides an example of `Array.fill`.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet28.fs)]

<span data-ttu-id="ba69f-243">Выходные данные выглядят следующим образом.</span><span class="sxs-lookup"><span data-stu-id="ba69f-243">The output is as follows.</span></span>

```
[|1; 2; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 23; 24; 25|]
```

<span data-ttu-id="ba69f-244">Можно использовать [ `Array.blit` ](https://msdn.microsoft.com/library/675e13e4-7fb9-4e0d-a5be-a112830de667) можно скопировать из одного массива в другой массив.</span><span class="sxs-lookup"><span data-stu-id="ba69f-244">You can use [`Array.blit`](https://msdn.microsoft.com/library/675e13e4-7fb9-4e0d-a5be-a112830de667) to copy a subsection of one array to another array.</span></span>

### <a name="converting-to-and-from-other-types"></a><span data-ttu-id="ba69f-245">Преобразование в и из других типов</span><span class="sxs-lookup"><span data-stu-id="ba69f-245">Converting to and from Other Types</span></span>

<span data-ttu-id="ba69f-246">[`Array.ofList`](https://msdn.microsoft.com/library/e7225239-f561-45a4-b0b5-69a1cdcae78b)Создает массив из списка.</span><span class="sxs-lookup"><span data-stu-id="ba69f-246">[`Array.ofList`](https://msdn.microsoft.com/library/e7225239-f561-45a4-b0b5-69a1cdcae78b) creates an array from a list.</span></span> <span data-ttu-id="ba69f-247">[`Array.ofSeq`](https://msdn.microsoft.com/library/6bedf5e0-4b22-46da-b09c-6aa09eff220c)Создает массив из последовательности.</span><span class="sxs-lookup"><span data-stu-id="ba69f-247">[`Array.ofSeq`](https://msdn.microsoft.com/library/6bedf5e0-4b22-46da-b09c-6aa09eff220c) creates an array from a sequence.</span></span> <span data-ttu-id="ba69f-248">[`Array.toList`](https://msdn.microsoft.com/library/4deff724-0be4-4688-92e7-9d67a1097786)и [ `Array.toSeq` ](https://msdn.microsoft.com/library/ac28dbab-406c-4fe0-ab08-c1ce5e247af4) на эти другие типы коллекций выполнить преобразование из типа массива.</span><span class="sxs-lookup"><span data-stu-id="ba69f-248">[`Array.toList`](https://msdn.microsoft.com/library/4deff724-0be4-4688-92e7-9d67a1097786) and [`Array.toSeq`](https://msdn.microsoft.com/library/ac28dbab-406c-4fe0-ab08-c1ce5e247af4) convert to these other collection types from the array type.</span></span>

### <a name="sorting-arrays"></a><span data-ttu-id="ba69f-249">Сортировка массивов</span><span class="sxs-lookup"><span data-stu-id="ba69f-249">Sorting Arrays</span></span>

<span data-ttu-id="ba69f-250">Используйте [ `Array.sort` ](https://msdn.microsoft.com/library/c6679075-e7eb-463c-9be5-c89be140c312) для сортировки массива с помощью универсальной функции сравнения.</span><span class="sxs-lookup"><span data-stu-id="ba69f-250">Use [`Array.sort`](https://msdn.microsoft.com/library/c6679075-e7eb-463c-9be5-c89be140c312) to sort an array by using the generic comparison function.</span></span> <span data-ttu-id="ba69f-251">Используйте [ `Array.sortBy` ](https://msdn.microsoft.com/library/144498dc-091d-4575-a229-c0bcbd61426b) для указания функция, которая создает значение, называется *ключ*, сортировка с помощью универсальной функции сравнения по ключу.</span><span class="sxs-lookup"><span data-stu-id="ba69f-251">Use [`Array.sortBy`](https://msdn.microsoft.com/library/144498dc-091d-4575-a229-c0bcbd61426b) to specify a function that generates a value, referred to as a *key*, to sort by using the generic comparison function on the key.</span></span> <span data-ttu-id="ba69f-252">Используйте [ `Array.sortWith` ](https://msdn.microsoft.com/library/699d3638-4244-4f42-8496-45f53d43ce95) Если вы хотите предоставить пользовательскую функцию сравнения.</span><span class="sxs-lookup"><span data-stu-id="ba69f-252">Use [`Array.sortWith`](https://msdn.microsoft.com/library/699d3638-4244-4f42-8496-45f53d43ce95) if you want to provide a custom comparison function.</span></span> <span data-ttu-id="ba69f-253">`Array.sort`, `Array.sortBy`, и `Array.sortWith` возвращают упорядоченный массив в виде нового массива.</span><span class="sxs-lookup"><span data-stu-id="ba69f-253">`Array.sort`, `Array.sortBy`, and `Array.sortWith` all return the sorted array as a new array.</span></span> <span data-ttu-id="ba69f-254">Варианты [ `Array.sortInPlace` ](https://msdn.microsoft.com/library/36f39947-8a88-4823-9e9b-e9d838d292e0), [ `Array.sortInPlaceBy` ](https://msdn.microsoft.com/library/7fb9d2dd-d461-4c67-8b43-b5c59fc12c3f), и [ `Array.sortInPlaceWith` ](https://msdn.microsoft.com/library/454f9e11-972d-47a6-a854-8031cb0c7b0b) изменения существующего массива вместо возвращения нового.</span><span class="sxs-lookup"><span data-stu-id="ba69f-254">The variations [`Array.sortInPlace`](https://msdn.microsoft.com/library/36f39947-8a88-4823-9e9b-e9d838d292e0), [`Array.sortInPlaceBy`](https://msdn.microsoft.com/library/7fb9d2dd-d461-4c67-8b43-b5c59fc12c3f), and [`Array.sortInPlaceWith`](https://msdn.microsoft.com/library/454f9e11-972d-47a6-a854-8031cb0c7b0b) modify the existing array instead of returning a new one.</span></span>

### <a name="arrays-and-tuples"></a><span data-ttu-id="ba69f-255">Массивы и кортежи</span><span class="sxs-lookup"><span data-stu-id="ba69f-255">Arrays and Tuples</span></span>

<span data-ttu-id="ba69f-256">Функции [ `Array.zip` ](https://msdn.microsoft.com/library/23e086b8-b266-4db2-8b68-e88e6a8e2187) и [ `Array.unzip` ](https://msdn.microsoft.com/library/a529b47c-2e2b-4f79-ad44-c578432d2f48) преобразуют массивы пар кортежей в кортежи массивов и наоборот.</span><span class="sxs-lookup"><span data-stu-id="ba69f-256">The functions [`Array.zip`](https://msdn.microsoft.com/library/23e086b8-b266-4db2-8b68-e88e6a8e2187) and [`Array.unzip`](https://msdn.microsoft.com/library/a529b47c-2e2b-4f79-ad44-c578432d2f48) convert arrays of tuple pairs to tuples of arrays and vice versa.</span></span> <span data-ttu-id="ba69f-257">[`Array.zip3`](https://msdn.microsoft.com/library/1745744a-d2ca-4c3e-b825-3f15d9f4000d)и [ `Array.unzip3` ](https://msdn.microsoft.com/library/bc3e6db0-f334-444f-8c30-813942880677) похожи за тем исключением, что они работают с кортежей из трех элементов или трех массивов.</span><span class="sxs-lookup"><span data-stu-id="ba69f-257">[`Array.zip3`](https://msdn.microsoft.com/library/1745744a-d2ca-4c3e-b825-3f15d9f4000d) and [`Array.unzip3`](https://msdn.microsoft.com/library/bc3e6db0-f334-444f-8c30-813942880677) are similar except that they work with tuples of three elements or tuples of three arrays.</span></span>

## <a name="parallel-computations-on-arrays"></a><span data-ttu-id="ba69f-258">Параллельные вычисления с массивами</span><span class="sxs-lookup"><span data-stu-id="ba69f-258">Parallel Computations on Arrays</span></span>

<span data-ttu-id="ba69f-259">Модуль [ `Array.Parallel` ](https://msdn.microsoft.com/library/60f30b77-5af4-4050-9a5c-bcdb3f5cbb09) содержит функции для выполнения параллельных вычислений с массивами.</span><span class="sxs-lookup"><span data-stu-id="ba69f-259">The module [`Array.Parallel`](https://msdn.microsoft.com/library/60f30b77-5af4-4050-9a5c-bcdb3f5cbb09) contains functions for performing parallel computations on arrays.</span></span> <span data-ttu-id="ba69f-260">Этот модуль не доступен для приложений, предназначенных для версий .NET Framework, предшествующих версии 4.</span><span class="sxs-lookup"><span data-stu-id="ba69f-260">This module is not available in applications that target versions of the .NET Framework prior to version 4.</span></span>

## <a name="see-also"></a><span data-ttu-id="ba69f-261">См. также</span><span class="sxs-lookup"><span data-stu-id="ba69f-261">See Also</span></span>
[<span data-ttu-id="ba69f-262">Справочник по языку F#</span><span class="sxs-lookup"><span data-stu-id="ba69f-262">F# Language Reference</span></span>](index.md)

[<span data-ttu-id="ba69f-263">F #; Типы</span><span class="sxs-lookup"><span data-stu-id="ba69f-263">F#; Types</span></span>](fsharp-types.md)