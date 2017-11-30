---
title: "Выражения запросов (F#)"
description: "Дополнительные сведения о поддержке выражения запроса LINQ в языке F #."
keywords: "visual f#, f#, функциональное программирование"
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 35df2d80-e6d2-4873-b2de-9b45b9e9e650
ms.openlocfilehash: 360733d81f049cd4356ecc47a27f97c3ec3a402a
ms.sourcegitcommit: bbde43da655ae7bea1977f7af7345eb87bd7fd5f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/21/2017
---
# <a name="query-expressions"></a><span data-ttu-id="e35f0-104">Выражения запросов</span><span class="sxs-lookup"><span data-stu-id="e35f0-104">Query Expressions</span></span>

> [!NOTE]
<span data-ttu-id="e35f0-105">Ссылки на справочник по API в этой статье ведут на сайт MSDN.</span><span class="sxs-lookup"><span data-stu-id="e35f0-105">The API reference links in this article will take you to MSDN.</span></span>  <span data-ttu-id="e35f0-106">Работа над справочником по API docs.microsoft.com не завершена.</span><span class="sxs-lookup"><span data-stu-id="e35f0-106">The docs.microsoft.com API reference is not complete.</span></span>

<span data-ttu-id="e35f0-107">Выражения запросов позволяют отправлять запросы к источнику данных и поместить их в нужную форму.</span><span class="sxs-lookup"><span data-stu-id="e35f0-107">Query expressions enable you to query a data source and put the data in a desired form.</span></span> <span data-ttu-id="e35f0-108">Выражения запросов обеспечивают поддержку LINQ в F #.</span><span class="sxs-lookup"><span data-stu-id="e35f0-108">Query expressions provide support for LINQ in F#.</span></span>

## <a name="syntax"></a><span data-ttu-id="e35f0-109">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="e35f0-109">Syntax</span></span>

```fsharp
query { expression }
```

## <a name="remarks"></a><span data-ttu-id="e35f0-110">Примечания</span><span class="sxs-lookup"><span data-stu-id="e35f0-110">Remarks</span></span>
<span data-ttu-id="e35f0-111">Выражения запроса — это разновидность вычислительное выражение аналогично выражения последовательности.</span><span class="sxs-lookup"><span data-stu-id="e35f0-111">Query expressions are a type of computation expression similar to sequence expressions.</span></span> <span data-ttu-id="e35f0-112">Так же, как указать последовательность, предоставив код в выражении последовательности, добавив код в выражении запроса указывается набор данных.</span><span class="sxs-lookup"><span data-stu-id="e35f0-112">Just as you specify a sequence by providing code in a sequence expression, you specify a set of data by providing code in a query expression.</span></span> <span data-ttu-id="e35f0-113">В выражении последовательности `yield` ключевое слово определяет данные, возвращаемые как часть результирующей последовательности.</span><span class="sxs-lookup"><span data-stu-id="e35f0-113">In a sequence expression, the `yield` keyword identifies data to be returned as part of the resulting sequence.</span></span> <span data-ttu-id="e35f0-114">В выражениях запросов `select` ключевое слово выполняет ту же функцию.</span><span class="sxs-lookup"><span data-stu-id="e35f0-114">In query expressions, the `select` keyword performs the same function.</span></span> <span data-ttu-id="e35f0-115">В дополнение к `select` ключевое слово, F # также поддерживает несколько операторов запросов, которые являются очень похоже на части инструкции SQL SELECT.</span><span class="sxs-lookup"><span data-stu-id="e35f0-115">In addition to the `select` keyword, F# also supports a number of query operators that are much like the parts of a SQL SELECT statement.</span></span> <span data-ttu-id="e35f0-116">Ниже приведен пример выражения простой запрос, вместе с кодом, который подключается к источнику OData «Борей».</span><span class="sxs-lookup"><span data-stu-id="e35f0-116">Here is an example of a simple query expression, along with code that connects to the Northwind OData source.</span></span>

```fsharp
// Use the OData type provider to create types that can be used to access the Northwind database.
// Add References to FSharp.Data.TypeProviders and System.Data.Services.Client
open Microsoft.FSharp.Data.TypeProviders

type Northwind = ODataService<"http://services.odata.org/Northwind/Northwind.svc">
let db = Northwind.GetDataContext()

// A query expression.
let query1 =
    query {
        for customer in db.Customers do
            select customer
    }

// Print results
query1
|> Seq.iter (fun customer -> printfn "Company: %s Contact: %s" customer.CompanyName customer.ContactName)
```

<span data-ttu-id="e35f0-117">В предыдущем примере выражение запроса состоит в фигурные скобки.</span><span class="sxs-lookup"><span data-stu-id="e35f0-117">In the previous code example, the query expression is in curly braces.</span></span> <span data-ttu-id="e35f0-118">Значение кода в выражении, возвращают каждого клиента в таблице Customers в базе данных в результатах запроса.</span><span class="sxs-lookup"><span data-stu-id="e35f0-118">The meaning of the code in the expression is, return every customer in the Customers table in the database in the query results.</span></span> <span data-ttu-id="e35f0-119">Выражения запросов возвращать тип, реализующий <xref:System.Linq.IQueryable%601> и <xref:System.Collections.Generic.IEnumerable%601>, и поэтому их можно выполнить итерацию с помощью [Seq-модуль](https://msdn.microsoft.com/library/54e8f059-ca52-4632-9ae9-49685ee9b684) как показано в примере.</span><span class="sxs-lookup"><span data-stu-id="e35f0-119">Query expressions return a type that implements <xref:System.Linq.IQueryable%601> and <xref:System.Collections.Generic.IEnumerable%601>, and so they can be iterated using the [Seq module](https://msdn.microsoft.com/library/54e8f059-ca52-4632-9ae9-49685ee9b684) as the example shows.</span></span>

<span data-ttu-id="e35f0-120">Каждый тип вычисления выражения состоит из класс построителя.</span><span class="sxs-lookup"><span data-stu-id="e35f0-120">Every computation expression type is built from a builder class.</span></span> <span data-ttu-id="e35f0-121">Класс построителя для вычислительного выражения запроса — `QueryBuilder`.</span><span class="sxs-lookup"><span data-stu-id="e35f0-121">The builder class for the query computation expression is `QueryBuilder`.</span></span> <span data-ttu-id="e35f0-122">Дополнительные сведения см. в разделе [вычислительных выражениях](computation-expressions.md) и [класс Linq.QueryBuilder](https://msdn.microsoft.com/visualfsharpdocs/conceptual/linq.querybuilder-class-%5bfsharp%5d).</span><span class="sxs-lookup"><span data-stu-id="e35f0-122">For more information, see [Computation Expressions](computation-expressions.md) and [Linq.QueryBuilder Class](https://msdn.microsoft.com/visualfsharpdocs/conceptual/linq.querybuilder-class-%5bfsharp%5d).</span></span>


## <a name="query-operators"></a><span data-ttu-id="e35f0-123">Операторы запроса</span><span class="sxs-lookup"><span data-stu-id="e35f0-123">Query Operators</span></span>
<span data-ttu-id="e35f0-124">Операторы запросов позволяют указать подробные сведения запроса, такие как поместить критерии для возвращаемых записей или указать порядок сортировки результатов.</span><span class="sxs-lookup"><span data-stu-id="e35f0-124">Query operators enable you to specify the details of the query, such as to put criteria on records to be returned, or specify the sorting order of results.</span></span> <span data-ttu-id="e35f0-125">Источник запроса должен поддерживать оператор запроса.</span><span class="sxs-lookup"><span data-stu-id="e35f0-125">The query source must support the query operator.</span></span> <span data-ttu-id="e35f0-126">При попытке использовать оператор не поддерживается запроса `System.NotSupportedException` будет создано.</span><span class="sxs-lookup"><span data-stu-id="e35f0-126">If you attempt to use an unsupported query operator, `System.NotSupportedException` will be thrown.</span></span>

<span data-ttu-id="e35f0-127">В выражениях запросов допускаются только выражения, которые могут быть преобразованы в SQL.</span><span class="sxs-lookup"><span data-stu-id="e35f0-127">Only expressions that can be translated to SQL are allowed in query expressions.</span></span> <span data-ttu-id="e35f0-128">Например, вызов функции не допускаются в выражениях при использовании `where` оператора запроса.</span><span class="sxs-lookup"><span data-stu-id="e35f0-128">For example, no function calls are allowed in the expressions when you use the `where` query operator.</span></span>

<span data-ttu-id="e35f0-129">Таблице 1 показаны доступные операторы.</span><span class="sxs-lookup"><span data-stu-id="e35f0-129">Table 1 shows available query operators.</span></span> <span data-ttu-id="e35f0-130">Кроме того см. в таблице Table2, который сравнивает запросы SQL и эквивалентные выражения запросов F # далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="e35f0-130">In addition, see Table2, which compares SQL queries and the equivalent F# query expressions later in this topic.</span></span> <span data-ttu-id="e35f0-131">Некоторые операторы запросов не поддерживаются некоторые поставщики типов.</span><span class="sxs-lookup"><span data-stu-id="e35f0-131">Some query operators aren't supported by some type providers.</span></span> <span data-ttu-id="e35f0-132">В частности в операторах запросов, которые она поддерживает из-за ограничений OData ограничен поставщик типов OData.</span><span class="sxs-lookup"><span data-stu-id="e35f0-132">In particular, the OData type provider is limited in the query operators that it supports due to limitations in OData.</span></span> <span data-ttu-id="e35f0-133">Дополнительные сведения см. в разделе [поставщика типов ODataService (F #)](https://msdn.microsoft.com/library/bac609dd-9d12-4bf9-a662-24bdf4faa43e).</span><span class="sxs-lookup"><span data-stu-id="e35f0-133">For more information, see [ODataService Type Provider (F#)](https://msdn.microsoft.com/library/bac609dd-9d12-4bf9-a662-24bdf4faa43e).</span></span>

<span data-ttu-id="e35f0-134">В этой таблице предполагается базы данных в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="e35f0-134">This table assumes a database in the following form:</span></span>

![Пример диаграммы базы данных](../media/StudentCourseDB.png)

<span data-ttu-id="e35f0-136">В следующей таблице также предполагается, в следующем примере кода подключения базы данных.</span><span class="sxs-lookup"><span data-stu-id="e35f0-136">The code in the tables that follow also assumes the following database connection code.</span></span> <span data-ttu-id="e35f0-137">Проекты следует добавить ссылки на сборки System.Drawing, System.Data.Linq и FSharp.Data.TypeProviders.</span><span class="sxs-lookup"><span data-stu-id="e35f0-137">Projects should add references to System.Data,  System.Data.Linq, and FSharp.Data.TypeProviders assemblies.</span></span> <span data-ttu-id="e35f0-138">Код, который создает эта база данных приведен в конце этого раздела.</span><span class="sxs-lookup"><span data-stu-id="e35f0-138">The code that creates this database is included at the end of this topic.</span></span>

```fsharp
open System
open Microsoft.FSharp.Data.TypeProviders
open System.Data.Linq.SqlClient
open System.Linq
open Microsoft.FSharp.Linq

type schema = SqlDataConnection< @"Data Source=SERVER\INSTANCE;Initial Catalog=MyDatabase;Integrated Security=SSPI;" >

let db = schema.GetDataContext()

// Needed for some query operator examples:
let data = [ 1; 5; 7; 11; 18; 21]
```

### <a name="table-1-query-operators"></a><span data-ttu-id="e35f0-139">Таблица 1.</span><span class="sxs-lookup"><span data-stu-id="e35f0-139">Table 1.</span></span> <span data-ttu-id="e35f0-140">Операторы запроса</span><span class="sxs-lookup"><span data-stu-id="e35f0-140">Query Operators</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="e35f0-141">Оператор</span><span class="sxs-lookup"><span data-stu-id="e35f0-141">Operator</span></span></th>
    <th><span data-ttu-id="e35f0-142">Описание</span><span class="sxs-lookup"><span data-stu-id="e35f0-142">Description</span></span></th>
  </tr>
  <tr>
  <td>`contains`</td>
<td><span data-ttu-id="e35f0-143">Определяет, включать ли выбранных элементов указанного элемента.</span><span class="sxs-lookup"><span data-stu-id="e35f0-143">Determines whether the selected elements include a specified element.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    select student.Age.Value
    contains 11
}
</code></pre>

</td>
</tr>


<tr>
  <td>`count`</td><td><span data-ttu-id="e35f0-144">Возвращает число выбранных элементов.</span><span class="sxs-lookup"><span data-stu-id="e35f0-144">Returns the number of selected elements.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    select student
    count
}
</code></pre>

</td></tr><tr>
<td>`last`</td><td><span data-ttu-id="e35f0-145">Выбирает последний элемент выбранных в данный момент.</span><span class="sxs-lookup"><span data-stu-id="e35f0-145">Selects the last element of those selected so far.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for number in data do
    last
}
</code></pre>

</td></tr><tr>
<td>`lastOrDefault`</td><td><span data-ttu-id="e35f0-146">Выбирает последний элемент выбранных в данный момент, или значение по умолчанию, если элемент не найден.</span><span class="sxs-lookup"><span data-stu-id="e35f0-146">Selects the last element of those selected so far, or a default value if no element is found.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for number in data do
    where (number < 0)
    lastOrDefault
}
</code></pre>

</td></tr><tr>
<td>`exactlyOne`</td><td><span data-ttu-id="e35f0-147">Выбирает конкретную элемент, выбранный в данный момент.</span><span class="sxs-lookup"><span data-stu-id="e35f0-147">Selects the single, specific element selected so far.</span></span> <span data-ttu-id="e35f0-148">При наличии нескольких элементов, создается исключение.</span><span class="sxs-lookup"><span data-stu-id="e35f0-148">If multiple elements are present, an exception is thrown.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    where (student.StudentID = 1)
    select student
    exactlyOne
}
</code></pre>

</td></tr><tr>
<td>`exactlyOneOrDefault`</td><td><span data-ttu-id="e35f0-149">Выбирает один конкретный элемент из выбранных в данный момент, или значение по умолчанию, если этот элемент не найден.</span><span class="sxs-lookup"><span data-stu-id="e35f0-149">Selects the single, specific element of those selected so far, or a default value if that element is not found.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    where (student.StudentID = 1)
    select student
    exactlyOneOrDefault
}
</code></pre>

</td></tr><tr>
<td>`headOrDefault`</td><td><span data-ttu-id="e35f0-150">Выбирает первый элемент выбранных в данный момент, или значение по умолчанию, если последовательность не содержит элементов.</span><span class="sxs-lookup"><span data-stu-id="e35f0-150">Selects the first element of those selected so far, or a default value if the sequence contains no elements.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    select student
    headOrDefault
}
</code></pre>

</td></tr><tr>
<td>`select`</td><td><span data-ttu-id="e35f0-151">Проецирует каждый из элементов, выбранных в данный момент.</span><span class="sxs-lookup"><span data-stu-id="e35f0-151">Projects each of the elements selected so far.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    select student
}
</code></pre>

</td></tr><tr>
<td>`where`</td><td><span data-ttu-id="e35f0-152">Выбирает элементы на основе заданного предиката.</span><span class="sxs-lookup"><span data-stu-id="e35f0-152">Selects elements based on a specified predicate.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    where (student.StudentID > 4)
    select student
}
</code></pre>

</td></tr><tr>
<td>`minBy`</td><td><span data-ttu-id="e35f0-153">Выбирает значение для каждого элемента, выбранного в данный момент и возвращает минимальное результирующее значение.</span><span class="sxs-lookup"><span data-stu-id="e35f0-153">Selects a value for each element selected so far and returns the minimum resulting value.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    minBy student.StudentID
}
</code></pre>

</td></tr><tr>
<td>`maxBy`</td><td><span data-ttu-id="e35f0-154">Выбирает значение для каждого элемента, выбранного в данный момент и возвращает максимальное значение.</span><span class="sxs-lookup"><span data-stu-id="e35f0-154">Selects a value for each element selected so far and returns the maximum resulting value.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    maxBy student.StudentID
}
</code></pre>

</td></tr><tr>
<td>`groupBy`</td><td><span data-ttu-id="e35f0-155">Группы элементов, выбранных в данный момент в соответствии с указанной функцией выбора ключа.</span><span class="sxs-lookup"><span data-stu-id="e35f0-155">Groups the elements selected so far according to a specified key selector.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    groupBy student.Age into g
    select (g.Key, g.Count())
}
</code></pre>

</td></tr><tr>
<td>`sortBy`</td><td><span data-ttu-id="e35f0-156">Сортирует элементы, пока выбран в порядке возрастания по данного ключа сортировки.</span><span class="sxs-lookup"><span data-stu-id="e35f0-156">Sorts the elements selected so far in ascending order by the given sorting key.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    sortBy student.Name
    select student
}
</code></pre>

</td></tr><tr>
<td>`sortByDescending`</td><td><span data-ttu-id="e35f0-157">Сортирует элементы, пока выбран в убывающем порядке по данного ключа сортировки.</span><span class="sxs-lookup"><span data-stu-id="e35f0-157">Sorts the elements selected so far in descending order by the given sorting key.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    sortByDescending student.Name
    select student
}
</code></pre>

</td></tr><tr>
<td>`thenBy`</td><td><span data-ttu-id="e35f0-158">Выполняет дополнительное упорядочение элементов, пока выбран в порядке возрастания по данного ключа сортировки.</span><span class="sxs-lookup"><span data-stu-id="e35f0-158">Performs a subsequent ordering of the elements selected so far in ascending order by the given sorting key.</span></span> <span data-ttu-id="e35f0-159">Этот оператор можно использовать только после `sortBy`, `sortByDescending`, `thenBy`, или `thenByDescending`.</span><span class="sxs-lookup"><span data-stu-id="e35f0-159">This operator may only be used after a `sortBy`, `sortByDescending`, `thenBy`, or `thenByDescending`.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    where student.Age.HasValue
    sortBy student.Age.Value
    thenBy student.Name
    select student
}
</code></pre>

</td></tr><tr>
<td>`thenByDescending`</td><td><span data-ttu-id="e35f0-160">Выполняет дополнительное упорядочение элементов, пока выбран в убывающем порядке по данного ключа сортировки.</span><span class="sxs-lookup"><span data-stu-id="e35f0-160">Performs a subsequent ordering of the elements selected so far in descending order by the given sorting key.</span></span> <span data-ttu-id="e35f0-161">Этот оператор можно использовать только после `sortBy`, `sortByDescending`, `thenBy`, или `thenByDescending`.</span><span class="sxs-lookup"><span data-stu-id="e35f0-161">This operator may only be used after a `sortBy`, `sortByDescending`, `thenBy`, or `thenByDescending`.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    where student.Age.HasValue
    sortBy student.Age.Value
    thenByDescending student.Name
    select student
}
</code></pre>

</td></tr><tr>
<td>`groupValBy`</td><td><span data-ttu-id="e35f0-162">Выбирает значение для каждого элемента, выбранного в данный момент и группирует элементы с указанным ключом.</span><span class="sxs-lookup"><span data-stu-id="e35f0-162">Selects a value for each element selected so far and groups the elements by the given key.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    groupValBy student.Name student.Age into g
    select (g, g.Key, g.Count())
}
</code></pre>

</td></tr><tr>
<td>`join`</td><td><span data-ttu-id="e35f0-163">Корреляции между двумя наборами выбранных значений на основе сопоставления ключей.</span><span class="sxs-lookup"><span data-stu-id="e35f0-163">Correlates two sets of selected values based on matching keys.</span></span> <span data-ttu-id="e35f0-164">Обратите внимание, что порядок следования ключей вокруг = вход в выражении соединения имеет значение.</span><span class="sxs-lookup"><span data-stu-id="e35f0-164">Note that the order of the keys around the = sign in a join expression is significant.</span></span> <span data-ttu-id="e35f0-165">В все соединения, если строка разбивается после `-&gt;` символа, отступы необходимо отступом по крайней мере настолько, насколько ключевое слово `for`.</span><span class="sxs-lookup"><span data-stu-id="e35f0-165">In all joins, if the line is split after the `-&gt;` symbol, the indentation must be indented at least as far as the keyword `for`.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    join selection in db.CourseSelection
        on (student.StudentID = selection.StudentID)
    select (student, selection)
}
</code></pre>

</td></tr><tr>
<td>`groupJoin`</td><td><span data-ttu-id="e35f0-166">Корреляции между двумя наборами выбранных значений на основе сопоставления ключей и группирует результаты.</span><span class="sxs-lookup"><span data-stu-id="e35f0-166">Correlates two sets of selected values based on matching keys and groups the results.</span></span> <span data-ttu-id="e35f0-167">Обратите внимание, что порядок следования ключей вокруг = вход в выражении соединения имеет значение.</span><span class="sxs-lookup"><span data-stu-id="e35f0-167">Note that the order of the keys around the = sign in a join expression is significant.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    groupJoin courseSelection in db.CourseSelection
        on (student.StudentID = courseSelection.StudentID) into g
    for courseSelection in g do
    join course in db.Course
        on (courseSelection.CourseID = course.CourseID)
    select (student.Name, course.CourseName)
}
</code></pre>

</td></tr><tr>
<td>`leftOuterJoin`</td><td><span data-ttu-id="e35f0-168">Корреляции между двумя наборами выбранных значений на основе сопоставления ключей и группирует результаты.</span><span class="sxs-lookup"><span data-stu-id="e35f0-168">Correlates two sets of selected values based on matching keys and groups the results.</span></span> <span data-ttu-id="e35f0-169">Если любой группы является пустым, вместо него используется со значением по умолчанию одной группы.</span><span class="sxs-lookup"><span data-stu-id="e35f0-169">If any group is empty, a group with a single default value is used instead.</span></span> <span data-ttu-id="e35f0-170">Обратите внимание, что порядок следования ключей вокруг = вход в выражении соединения имеет значение.</span><span class="sxs-lookup"><span data-stu-id="e35f0-170">Note that the order of the keys around the = sign in a join expression is significant.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    leftOuterJoin selection in db.CourseSelection
        on (student.StudentID = selection.StudentID) into result
    for selection in result.DefaultIfEmpty() do
    select (student, selection)
}
</code></pre>

</td></tr><tr>
<td>`sumByNullable`</td><td><span data-ttu-id="e35f0-171">Допускает значения NULL значение для каждого элемента, выбранного в данный момент выбирает и возвращает сумму этих значений.</span><span class="sxs-lookup"><span data-stu-id="e35f0-171">Selects a nullable value for each element selected so far and returns the sum of these values.</span></span> <span data-ttu-id="e35f0-172">Если все значения NULL не имеет значения, он игнорируется.</span><span class="sxs-lookup"><span data-stu-id="e35f0-172">If any nullable does not have a value, it is ignored.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    sumByNullable student.Age
}
</code></pre>

</td></tr><tr>
<td>`minByNullable`</td><td><span data-ttu-id="e35f0-173">Выбирает значение допускает значения NULL для каждого элемента, выбранного в данный момент и возвращает минимальный из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="e35f0-173">Selects a nullable value for each element selected so far and returns the minimum of these values.</span></span> <span data-ttu-id="e35f0-174">Если все значения NULL не имеет значения, он игнорируется.</span><span class="sxs-lookup"><span data-stu-id="e35f0-174">If any nullable does not have a value, it is ignored.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    minByNullable student.Age
}
</code></pre>

</td></tr><tr>
<td>`maxByNullable`</td><td><span data-ttu-id="e35f0-175">Допускает значения NULL значение для каждого элемента, выбранного в данный момент выбирает и возвращает максимальное значение из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="e35f0-175">Selects a nullable value for each element selected so far and returns the maximum of these values.</span></span> <span data-ttu-id="e35f0-176">Если все значения NULL не имеет значения, он игнорируется.</span><span class="sxs-lookup"><span data-stu-id="e35f0-176">If any nullable does not have a value, it is ignored.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    maxByNullable student.Age
}
</code></pre>

</td></tr><tr>
<td>`averageByNullable`</td><td><span data-ttu-id="e35f0-177">Допускает значения NULL значение для каждого элемента, выбранного в данный момент выбирает и возвращает среднее значение из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="e35f0-177">Selects a nullable value for each element selected so far and returns the average of these values.</span></span> <span data-ttu-id="e35f0-178">Если все значения NULL не имеет значения, он игнорируется.</span><span class="sxs-lookup"><span data-stu-id="e35f0-178">If any nullable does not have a value, it is ignored.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    averageByNullable (Nullable.float student.Age)
}
</code></pre>

</td></tr><tr>
<td>`averageBy`</td><td><span data-ttu-id="e35f0-179">Выбирает значение для каждого элемента, выбранного в данный момент и возвращает среднее значение из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="e35f0-179">Selects a value for each element selected so far and returns the average of these values.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    averageBy (float student.StudentID)
}
</code></pre>

</td></tr><tr>
<td>`distinct`</td><td><span data-ttu-id="e35f0-180">Выбирает различающиеся элементы из элементов, выбранных в данный момент.</span><span class="sxs-lookup"><span data-stu-id="e35f0-180">Selects distinct elements from the elements selected so far.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    join selection in db.CourseSelection
        on (student.StudentID = selection.StudentID)
    distinct       
}
</code></pre>

</td></tr><tr>
<td>`exists`</td><td><span data-ttu-id="e35f0-181">Определяет, удовлетворяет ли любой элемент, выбранный в данный момент условие.</span><span class="sxs-lookup"><span data-stu-id="e35f0-181">Determines whether any element selected so far satisfies a condition.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    where
        (query {
            for courseSelection in db.CourseSelection do
            exists (courseSelection.StudentID = student.StudentID) })
    select student
}
</code></pre>

</td></tr><tr>
<td>`find`</td><td><span data-ttu-id="e35f0-182">Выбирает первый элемент, выбранного в данный момент, удовлетворяющий указанному условию.</span><span class="sxs-lookup"><span data-stu-id="e35f0-182">Selects the first element selected so far that satisfies a specified condition.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    find (student.Name = "Abercrombie, Kim")
}
</code></pre>

</td></tr><tr>
<td>`all`</td><td><span data-ttu-id="e35f0-183">Определяет, является ли все элементы, выбранные в данный момент удовлетворяют условию.</span><span class="sxs-lookup"><span data-stu-id="e35f0-183">Determines whether all elements selected so far satisfy a condition.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    all (SqlMethods.Like(student.Name, "%,%"))
}
</code></pre>

</td></tr><tr>
<td>`head`</td><td><span data-ttu-id="e35f0-184">Выбирает первый элемент из выбранных в данный момент.</span><span class="sxs-lookup"><span data-stu-id="e35f0-184">Selects the first element from those selected so far.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    head
}
</code></pre>

</td></tr><tr>
<td>`nth`</td><td><span data-ttu-id="e35f0-185">Выбирает элемент по указанному индексу среди выбранных к текущему моменту.</span><span class="sxs-lookup"><span data-stu-id="e35f0-185">Selects the element at a specified index amongst those selected so far.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for numbers in data do
    nth 3
}
</code></pre>

</td></tr><tr>
<td>`skip`</td><td><span data-ttu-id="e35f0-186">Пропускает указанного число элементов, выбранных в данный момент, а затем выбирает оставшиеся элементы.</span><span class="sxs-lookup"><span data-stu-id="e35f0-186">Bypasses a specified number of the elements selected so far and then selects the remaining elements.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    skip 1
}
</code></pre>

</td></tr><tr>
<td>`skipWhile`</td><td><span data-ttu-id="e35f0-187">Пропускает элементы в последовательности, пока заданное условие имеет значение true, а затем выбирает оставшиеся элементы.</span><span class="sxs-lookup"><span data-stu-id="e35f0-187">Bypasses elements in a sequence as long as a specified condition is true and then selects the remaining elements.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for number in data do
    skipWhile (number < 3)
    select student
}
</code></pre>

</td></tr><tr>
<td>`sumBy`</td><td><span data-ttu-id="e35f0-188">Выбирает значение для каждого элемента, выбранного в данный момент и возвращает сумму этих значений.</span><span class="sxs-lookup"><span data-stu-id="e35f0-188">Selects a value for each element selected so far and returns the sum of these values.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    sumBy student.StudentID
}
</code></pre>

</td></tr><tr>
<td>`take`</td><td><span data-ttu-id="e35f0-189">Выбирает заданное число смежных элементов из выбранных к текущему моменту.</span><span class="sxs-lookup"><span data-stu-id="e35f0-189">Selects a specified number of contiguous elements from those selected so far.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    select student
    take 2
}
</code></pre>

</td></tr><tr>
<td>`takeWhile`</td><td><span data-ttu-id="e35f0-190">Выбор элементов из последовательности, пока заданное условие имеет значение true и затем пропускает оставшиеся элементы.</span><span class="sxs-lookup"><span data-stu-id="e35f0-190">Selects elements from a sequence as long as a specified condition is true, and then skips the remaining elements.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for number in data do
    takeWhile (number < 10)
}
</code></pre>

</td></tr><tr>
<td>`sortByNullable`</td><td><span data-ttu-id="e35f0-191">Сортирует элементы, пока выбран в порядке возрастания по данного ключа сортировки допускает значения NULL.</span><span class="sxs-lookup"><span data-stu-id="e35f0-191">Sorts the elements selected so far in ascending order by the given nullable sorting key.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    sortByNullable student.Age
    select student
}
</code></pre>

</td></tr><tr>
<td>`sortByNullableDescending`</td><td><span data-ttu-id="e35f0-192">Сортирует элементы, пока выбран в порядке убывания по данного ключа сортировки допускает значения NULL.</span><span class="sxs-lookup"><span data-stu-id="e35f0-192">Sorts the elements selected so far in descending order by the given nullable sorting key.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    sortByNullableDescending student.Age
    select student
}
</code></pre>

</td></tr><tr>
<td>`thenByNullable`</td><td><span data-ttu-id="e35f0-193">Выполняет дополнительное упорядочение элементов, пока выбран в порядке возрастания по данного ключа сортировки допускает значения NULL.</span><span class="sxs-lookup"><span data-stu-id="e35f0-193">Performs a subsequent ordering of the elements selected so far in ascending order by the given nullable sorting key.</span></span> <span data-ttu-id="e35f0-194">Этот оператор можно использовать только сразу после `sortBy`, `sortByDescending`, `thenBy`, или `thenByDescending`, либо от их вариантов, допускающие значение NULL.</span><span class="sxs-lookup"><span data-stu-id="e35f0-194">This operator may only be used immediately after a `sortBy`, `sortByDescending`, `thenBy`, or `thenByDescending`, or their nullable variants.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    sortBy student.Name
    thenByNullable student.Age
    select student
}
</code></pre>

</td></tr><tr>
<td>`thenByNullableDescending`</td><td><span data-ttu-id="e35f0-195">Выполняет дополнительное упорядочение элементов, пока выбран в порядке убывания по данного ключа сортировки допускает значения NULL.</span><span class="sxs-lookup"><span data-stu-id="e35f0-195">Performs a subsequent ordering of the elements selected so far in descending order by the given nullable sorting key.</span></span> <span data-ttu-id="e35f0-196">Этот оператор можно использовать только сразу после `sortBy`, `sortByDescending`, `thenBy`, или `thenByDescending`, либо от их вариантов, допускающие значение NULL.</span><span class="sxs-lookup"><span data-stu-id="e35f0-196">This operator may only be used immediately after a `sortBy`, `sortByDescending`, `thenBy`, or `thenByDescending`, or their nullable variants.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    sortBy student.Name
    thenByNullableDescending student.Age
    select student
}
</code></pre>

</td></tr>
</table>

## <a name="comparison-of-transact-sql-and-f-query-expressions"></a><span data-ttu-id="e35f0-197">Сравнение выражений запросов Transact-SQL и F#</span><span class="sxs-lookup"><span data-stu-id="e35f0-197">Comparison of Transact-SQL and F# Query Expressions</span></span>
<span data-ttu-id="e35f0-198">Ниже приведены некоторые стандартные запросы Transact-SQL и их эквиваленты в языке F #.</span><span class="sxs-lookup"><span data-stu-id="e35f0-198">The following table shows some common Transact-SQL queries and their equivalents in F#.</span></span> <span data-ttu-id="e35f0-199">В этой таблице также предполагается той же базе данных, как в предыдущей таблице и тот же исходный код для настройки поставщика типов.</span><span class="sxs-lookup"><span data-stu-id="e35f0-199">The code in this table also assumes the same database as the previous table and the same initial code to set up the type provider.</span></span>


### <a name="table-2-transact-sql-and-f-query-expressions"></a><span data-ttu-id="e35f0-200">В таблице 2.</span><span class="sxs-lookup"><span data-stu-id="e35f0-200">Table 2.</span></span> <span data-ttu-id="e35f0-201">Выражения запросов Transact-SQL и F#</span><span class="sxs-lookup"><span data-stu-id="e35f0-201">Transact-SQL and F# Query Expressions</span></span>


<table style="width:100%">
  <tr>
    <th><span data-ttu-id="e35f0-202">Transact-SQL (без учета регистра)</span><span class="sxs-lookup"><span data-stu-id="e35f0-202">Transact-SQL (not case sensitive)</span></span></th>
    <th><span data-ttu-id="e35f0-203">F # выражения запроса (с учетом регистра)</span><span class="sxs-lookup"><span data-stu-id="e35f0-203">F# Query Expression (case sensitive)</span></span></th>
  </tr>
<tr><td>
<span data-ttu-id="e35f0-204">Выберите все поля из таблицы.</span><span class="sxs-lookup"><span data-stu-id="e35f0-204">Select all fields from table.</span></span></br>

<pre><code class="lang-sql">SELECT * FROM Student
</code></pre>

</td><td>
<pre><code class="lang-fsharp">// All students.
query {
    for student in db.Student do
    select student
}
</code></pre>

</td></tr>
<tr><td>
<span data-ttu-id="e35f0-205">Число записей в таблице.</span><span class="sxs-lookup"><span data-stu-id="e35f0-205">Count records in a table.</span></span><br/>

<pre><code class="lang-sql">SELECT COUNT( * ) FROM Student
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Count of students.
query {
    for student in db.Student do       
    count
}
</code></pre>

</td></tr><tr>
<td>`EXISTS`
</br>

<pre><code class="lang-sql">SELECT * FROM Student
WHERE EXISTS
  (SELECT * FROM CourseSelection
   WHERE CourseSelection.StudentID = Student.StudentID)
</code></pre>
</td>

<td>

<pre><code class="lang-fsharp">// Find students who have signed up at least one course.
query {
    for student in db.Student do
    where
        (query {
            for courseSelection in db.CourseSelection do
            exists (courseSelection.StudentID = student.StudentID) })
    select student
}
</code></pre>

</td></tr><tr>
<td><span data-ttu-id="e35f0-206">Группирование</span><span class="sxs-lookup"><span data-stu-id="e35f0-206">Grouping</span></span><br/>

<pre><code class="lang-sql">SELECT Student.Age, COUNT( * ) FROM Student
GROUP BY Student.Age
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Group by age and count.
query {
    for n in db.Student do
    groupBy n.Age into g
    select (g.Key, g.Count())
}
// OR
query {
    for n in db.Student do
    groupValBy n.Age n.Age into g
    select (g.Key, g.Count())
}
</code></pre>
</td></tr><tr><td>
<span data-ttu-id="e35f0-207">Группирование с условием.</span><span class="sxs-lookup"><span data-stu-id="e35f0-207">Grouping with condition.</span></span><br/>

<pre><code class="lang-sql">SELECT Student.Age, COUNT( * )
FROM Student
GROUP BY Student.Age
HAVING student.Age > 10
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Group students by age where age > 10.
query {
    for student in db.Student do
    groupBy student.Age into g
    where (g.Key.HasValue && g.Key.Value > 10)
    select (g.Key, g.Count())
}
</code></pre>

</td></tr><tr><td>
<span data-ttu-id="e35f0-208">Группирование с условием count.</span><span class="sxs-lookup"><span data-stu-id="e35f0-208">Grouping with count condition.</span></span><br/>

<pre><code class="lang-sql">SELECT Student.Age, COUNT( * )
FROM Student
GROUP BY Student.Age
HAVING COUNT( * ) > 1
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Group students by age and count number of students
// at each age with more than 1 student.
query {
    for student in db.Student do
    groupBy student.Age into group
    where (group.Count() > 1)
    select (group.Key, group.Count())
}
</code></pre>

</td></tr><tr><td>
<span data-ttu-id="e35f0-209">Группирование, инвентаризации и суммирования.</span><span class="sxs-lookup"><span data-stu-id="e35f0-209">Grouping, counting, and summing.</span></span><br/>

<pre><code class="lang-sql">SELECT Student.Age, COUNT( * ), SUM(Student.Age) as total
FROM Student
GROUP BY Student.Age
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Group students by age and sum ages.
query {
    for student in db.Student do
    groupBy student.Age into g       
    let total =
        query {
            for student in g do
            sumByNullable student.Age
        }
    select (g.Key, g.Count(), total)
}
</code></pre>

</td></tr><tr><td>
<span data-ttu-id="e35f0-210">Группирование, инвентаризации и упорядочение по количеству.</span><span class="sxs-lookup"><span data-stu-id="e35f0-210">Grouping, counting, and ordering by count.</span></span><br/>

<pre><code class="lang-sql">SELECT Student.Age, COUNT( * ) as myCount
FROM Student
GROUP BY Student.Age
HAVING COUNT( * ) > 1
ORDER BY COUNT( * ) DESC
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Group students by age, count number of students
// at each age, and display all with count > 1
// in descending order of count.
query {
    for student in db.Student do
    groupBy student.Age into g
    where (g.Count() > 1)       
    sortByDescending (g.Count())
    select (g.Key, g.Count())
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="e35f0-211">
`IN`набор указанных значений</span><span class="sxs-lookup"><span data-stu-id="e35f0-211">
`IN` a set of specified values</span></span><br/>

<pre><code class="lang-sql">SELECT *
FROM Student
WHERE Student.StudentID IN (1, 2, 5, 10)
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Select students where studentID is one of a given list.
let idQuery =
    query {
        for id in [1; 2; 5; 10] do
        select id
    }
query {
    for student in db.Student do
    where (idQuery.Contains(student.StudentID))
    select student
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="e35f0-212">
`LIKE` и `TOP`.</span><span class="sxs-lookup"><span data-stu-id="e35f0-212">
`LIKE` and `TOP`.</span></span><br/>

<pre><code class="lang-sql">-- '_e%' matches strings where the second character is 'e'
SELECT TOP 2 * FROM Student
WHERE Student.Name LIKE '_e%'
</code></pre>

</td><td>
<pre><code class="lang-fsharp">// Look for students with Name match _e% pattern and take first two.
query {
    for student in db.Student do
    where (SqlMethods.Like( student.Name, "_e%") )
    select student
    take 2
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="e35f0-213">
`LIKE`с шаблоном соответствовать набору.</span><span class="sxs-lookup"><span data-stu-id="e35f0-213">
`LIKE` with pattern match set.</span></span><br/>

<pre><code class="lang-sql">-- '[abc]%' matches strings where the first character is
-- 'a', 'b', 'c', 'A', 'B', or 'C'
SELECT * FROM Student
WHERE Student.Name LIKE '[abc]%'
</code></pre>
</td><td>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    where (SqlMethods.Like( student.Name, "[abc]%") )
    select student 
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="e35f0-214">
`LIKE`с шаблоном набор исключений.</span><span class="sxs-lookup"><span data-stu-id="e35f0-214">
`LIKE` with set exclusion pattern.</span></span><br/>

<pre><code class="lang-sql">-- '[^abc]%' matches strings where the first character is
-- not 'a', 'b', 'c', 'A', 'B', or 'C'
SELECT * FROM Student
WHERE Student.Name LIKE '[^abc]%'
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Look for students with name matching [^abc]%% pattern.
query {
    for student in db.Student do
    where (SqlMethods.Like( student.Name, "[^abc]%") )
    select student
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="e35f0-215">
`LIKE`на одном поле, но выберите другое поле.</span><span class="sxs-lookup"><span data-stu-id="e35f0-215">
`LIKE` on one field, but select a different field.</span></span><br/>

<pre><code class="lang-sql">SELECT StudentID AS ID FROM Student
WHERE Student.Name LIKE '[^abc]%'
</code></pre>

</td><td>

<pre><code class="lang-fsharp">query {
    for n in db.Student do
    where (SqlMethods.Like( n.Name, "[^abc]%") )
    select n.StudentID   
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="e35f0-216">`LIKE`, с поиск подстроки.</span><span class="sxs-lookup"><span data-stu-id="e35f0-216">`LIKE`, with substring search.</span></span><br/>

<pre><code class="lang-sql">SELECT * FROM Student
WHERE Student.Name like '%A%'
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Using Contains as a query filter.
query {
    for student in db.Student do
    where (student.Name.Contains("a"))
    select student
}
</code></pre>

</td></tr><tr><td>
<span data-ttu-id="e35f0-217">Простой `JOIN` с двумя таблицами.</span><span class="sxs-lookup"><span data-stu-id="e35f0-217">Simple `JOIN` with two tables.</span></span><br/>

<pre><code class="lang-sql">SELECT * FROM Student
JOIN CourseSelection
ON Student.StudentID = CourseSelection.StudentID
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Join Student and CourseSelection tables.
query {
    for student in db.Student do
    join selection in db.CourseSelection
        on (student.StudentID = selection.StudentID)
    select (student, selection)
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="e35f0-218">`LEFT JOIN`с двумя таблицами.</span><span class="sxs-lookup"><span data-stu-id="e35f0-218">`LEFT JOIN` with two tables.</span></span><br/>

<pre><code class="lang-sql">SELECT * FROM Student
LEFT JOIN CourseSelection
ON Student.StudentID = CourseSelection.StudentID
</code></pre>

</td><td>

<pre><code class="lang-fsharp">//Left Join Student and CourseSelection tables.
query {
    for student in db.Student do
    leftOuterJoin selection in db.CourseSelection
        on (student.StudentID = selection.StudentID) into result
    for selection in result.DefaultIfEmpty() do
    select (student, selection)
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="e35f0-219">`JOIN`с помощью`COUNT`</span><span class="sxs-lookup"><span data-stu-id="e35f0-219">`JOIN` with `COUNT`</span></span><br/>

<pre><code class="lang-sql">SELECT COUNT( * ) FROM Student
JOIN CourseSelection
ON Student.StudentID = CourseSelection.StudentID
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Join with count.
query {
    for n in db.Student do
    join e in db.CourseSelection
        on (n.StudentID = e.StudentID)
    count
}
</code></pre>

</td></tr><tr><td>`DISTINCT`<br/>

<pre><code class="lang-sql">SELECT DISTINCT StudentID FROM CourseSelection
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Join with distinct.
query {
    for student in db.Student do
    join selection in db.CourseSelection
        on (student.StudentID = selection.StudentID)
    distinct
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="e35f0-220">Числа различных объектов.</span><span class="sxs-lookup"><span data-stu-id="e35f0-220">Distinct count.</span></span><br/>

<pre><code class="lang-sql">SELECT DISTINCT COUNT(StudentID) FROM CourseSelection
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Join with distinct and count.
query {
    for n in db.Student do
    join e in db.CourseSelection
        on (n.StudentID = e.StudentID)
    distinct
    count
}
</code></pre>

</td></tr><tr><td>`BETWEEN`<br/>

<pre><code class="lang-sql">SELECT * FROM Student
WHERE Student.Age BETWEEN 10 AND 15
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Selecting students with ages between 10 and 15.
query {
    for student in db.Student do
    where (student.Age ?>= 10 && student.Age ?< 15)
    select student
}
</code></pre>

</td></tr><tr><td>`OR`<br/>

<pre><code class="lang-sql">SELECT * FROM Student
WHERE Student.Age = 11 OR Student.Age = 12
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Selecting students with age that's either 11 or 12.
query {
    for student in db.Student do
    where (student.Age.Value = 11 &#124;&#124; student.Age.Value = 12)
    select student
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="e35f0-221">`OR`При упорядочении</span><span class="sxs-lookup"><span data-stu-id="e35f0-221">`OR` with ordering</span></span><br/>

<pre><code class="lang-sql">SELECT * FROM Student
WHERE Student.Age = 12 OR Student.Age = 13
ORDER BY Student.Age DESC
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Selecting students in a certain age range and sorting.
query {
    for n in db.Student do
    where (n.Age.Value = 12 &#124;&#124; n.Age.Value = 13)
    sortByNullableDescending n.Age
    select n
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="e35f0-222">`TOP`, `OR`и их сортировки.</span><span class="sxs-lookup"><span data-stu-id="e35f0-222">`TOP`, `OR`, and ordering.</span></span><br/>

<pre><code class="lang-sql">SELECT TOP 2 student.Name FROM Student
WHERE Student.Age = 11 OR Student.Age = 12
ORDER BY Student.Name DESC
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Selecting students with certain ages,
// taking account of the possibility of nulls.
query {
    for student in db.Student do
    where
        ((student.Age.HasValue && student.Age.Value = 11) &#124;&#124;
         (student.Age.HasValue && student.Age.Value = 12))
    sortByDescending student.Name
    select student.Name
    take 2
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="e35f0-223">`UNION`двух запросов.</span><span class="sxs-lookup"><span data-stu-id="e35f0-223">`UNION` of two queries.</span></span><br/>

<pre><code class="lang-sql">SELECT * FROM Student
UNION
SELECT * FROM lastStudent
</code></pre>

</td><td>

<pre><code class="lang-fsharp">
let query1 =
    query {
        for n in db.Student do
        select (n.Name, n.Age)
    }

let query2 =
    query {
        for n in db.LastStudent do
        select (n.Name, n.Age)
    }

query2.Union (query1)
</code></pre>

</td></tr><tr><td><span data-ttu-id="e35f0-224">Пересечение двух запросов.</span><span class="sxs-lookup"><span data-stu-id="e35f0-224">Intersection of two queries.</span></span><br/>

<pre><code class="lang-sql">SELECT * FROM Student
INTERSECT
SELECT * FROM LastStudent
</code></pre>
</td><td>

<pre><code class="lang-fsharp">
let query1 =
    query {
        for n in db.Student do
        select (n.Name, n.Age)
    }

let query2 =
    query {
        for n in db.LastStudent do
        select (n.Name, n.Age)
    }

query1.Intersect(query2)
</code></pre>

</td></tr><tr><td><span data-ttu-id="e35f0-225">`CASE`условие.</span><span class="sxs-lookup"><span data-stu-id="e35f0-225">`CASE` condition.</span></span><br/>

<pre><code class="lang-sql">SELECT student.StudentID,
CASE Student.Age
  WHEN -1 THEN 100
  ELSE Student.Age
END,
Student.Age
FROM Student
</code></pre>

</td><td>
<pre><code class="lang-fsharp">// Using if statement to alter results for special value.
query {
    for student in db.Student do
    select
        (if student.Age.HasValue && student.Age.Value = -1 then
             (student.StudentID, System.Nullable<int>(100), student.Age)
         else (student.StudentID, student.Age, student.Age))
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="e35f0-226">Несколько вариантов.</span><span class="sxs-lookup"><span data-stu-id="e35f0-226">Multiple cases.</span></span><br/>

<pre><code class="lang-sql">SELECT Student.StudentID,
CASE Student.Age
  WHEN -1 THEN 100
  WHEN 0 THEN 1000
  ELSE Student.Age
END,
Student.Age
FROM Student
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Using if statement to alter results for special values.
query {
    for student in db.Student do
    select
        (if student.Age.HasValue && student.Age.Value = -1 then
             (student.StudentID, System.Nullable<int>(100), student.Age)
         elif student.Age.HasValue && student.Age.Value = 0 then
             (student.StudentID, System.Nullable<int>(1000), student.Age)
         else (student.StudentID, student.Age, student.Age))
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="e35f0-227">Несколько таблиц</span><span class="sxs-lookup"><span data-stu-id="e35f0-227">Multiple tables.</span></span><br/>

<pre><code class="lang-sql">SELECT * FROM Student, Course
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Multiple table select.
query {
    for student in db.Student do
    for course in db.Course do
    select (student, course)
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="e35f0-228">Несколько соединений.</span><span class="sxs-lookup"><span data-stu-id="e35f0-228">Multiple joins.</span></span><br/>

<pre><code class="lang-sql">SELECT Student.Name, Course.CourseName
FROM Student
JOIN CourseSelection
ON CourseSelection.StudentID = Student.StudentID
JOIN Course
ON Course.CourseID = CourseSelection.CourseID
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Multiple joins.
query {
    for student in db.Student do
    join courseSelection in db.CourseSelection
        on (student.StudentID = courseSelection.StudentID)
    join course in db.Course
        on (courseSelection.CourseID = course.CourseID)
    select (student.Name, course.CourseName)
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="e35f0-229">Несколько левые внешние соединения.</span><span class="sxs-lookup"><span data-stu-id="e35f0-229">Multiple left outer joins.</span></span><br/>

<pre><code class="lang-sql">SELECT Student.Name, Course.CourseName
FROM Student
LEFT OUTER JOIN CourseSelection
ON CourseSelection.StudentID = Student.StudentID
LEFT OUTER JOIN Course
ON Course.CourseID = CourseSelection.CourseID
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Using leftOuterJoin with multiple joins.
query {
    for student in db.Student do
    leftOuterJoin courseSelection in db.CourseSelection
        on (student.StudentID = courseSelection.StudentID) into g1
    for courseSelection in g1.DefaultIfEmpty() do
    leftOuterJoin course in db.Course
        on (courseSelection.CourseID = course.CourseID) into g2
    for course in g2.DefaultIfEmpty() do
    select (student.Name, course.CourseName)
}
</code></pre>

</td></tr></table>

<span data-ttu-id="e35f0-230">Следующий код может использоваться для создания образца базы данных для этих примеров.</span><span class="sxs-lookup"><span data-stu-id="e35f0-230">The following code can be used to create the sample database for these examples.</span></span>

<pre><code class="lang-sql">SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO

USE [master];
GO

IF EXISTS (SELECT * FROM sys.databases WHERE name = 'MyDatabase')
DROP DATABASE MyDatabase;
GO

-- Create the MyDatabase database.
CREATE DATABASE MyDatabase COLLATE SQL_Latin1_General_CP1_CI_AS;
GO

-- Specify a simple recovery model
-- to keep the log growth to a minimum.
ALTER DATABASE MyDatabase
SET RECOVERY SIMPLE;
GO

USE MyDatabase;
GO

CREATE TABLE [dbo].[Course] (
[CourseID]   INT           NOT NULL,
[CourseName] NVARCHAR (50) NOT NULL,
PRIMARY KEY CLUSTERED ([CourseID] ASC)
);

CREATE TABLE [dbo].[Student] (
[StudentID] INT           NOT NULL,
[Name]      NVARCHAR (50) NOT NULL,
[Age]       INT           NULL,
PRIMARY KEY CLUSTERED ([StudentID] ASC)
);

CREATE TABLE [dbo].[CourseSelection] (
[ID]        INT NOT NULL,
[StudentID] INT NOT NULL,
[CourseID]  INT NOT NULL,
PRIMARY KEY CLUSTERED ([ID] ASC),
CONSTRAINT [FK_CourseSelection_ToTable] FOREIGN KEY ([StudentID]) REFERENCES [dbo].[Student] ([StudentID]) ON DELETE NO ACTION ON UPDATE NO ACTION,
CONSTRAINT [FK_CourseSelection_Course_1] FOREIGN KEY ([CourseID]) REFERENCES [dbo].[Course] ([CourseID]) ON DELETE NO ACTION ON UPDATE NO ACTION
);

CREATE TABLE [dbo].[LastStudent] (
[StudentID] INT           NOT NULL,
[Name]      NVARCHAR (50) NOT NULL,
[Age]       INT           NULL,
PRIMARY KEY CLUSTERED ([StudentID] ASC)
);

-- Insert data into the tables.
USE MyDatabase
INSERT INTO Course (CourseID, CourseName)
VALUES(1, 'Algebra I');
INSERT INTO Course (CourseID, CourseName)
VALUES(2, 'Trigonometry');
INSERT INTO Course (CourseID, CourseName)
VALUES(3, 'Algebra II');
INSERT INTO Course (CourseID, CourseName)
VALUES(4, 'History');
INSERT INTO Course (CourseID, CourseName)
VALUES(5, 'English');
INSERT INTO Course (CourseID, CourseName)
VALUES(6, 'French');
INSERT INTO Course (CourseID, CourseName)
VALUES(7, 'Chinese');

INSERT INTO Student (StudentID, Name, Age)
VALUES(1, 'Abercrombie, Kim', 10);
INSERT INTO Student (StudentID, Name, Age)
VALUES(2, 'Abolrous, Hazen', 14);
INSERT INTO Student (StudentID, Name, Age)
VALUES(3, 'Hance, Jim', 12);
INSERT INTO Student (StudentID, Name, Age)
VALUES(4, 'Adams, Terry', 12);
INSERT INTO Student (StudentID, Name, Age)
VALUES(5, 'Hansen, Claus', 11);
INSERT INTO Student (StudentID, Name, Age)
VALUES(6, 'Penor, Lori', 13);
INSERT INTO Student (StudentID, Name, Age)
VALUES(7, 'Perham, Tom', 12);
INSERT INTO Student (StudentID, Name, Age)
VALUES(8, 'Peng, Yun-Feng', NULL);

INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(1, 1, 2);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(2, 1, 3);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(3, 1, 5);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(4, 2, 2);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(5, 2, 5);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(6, 2, 6);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(7, 2, 3);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(8, 3, 2);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(9, 3, 1);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(10, 4, 2);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(11, 4, 5);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(12, 4, 2);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(13, 5, 3);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(14, 5, 2);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(15, 7, 3);
</code></pre>

<span data-ttu-id="e35f0-231">Следующий код содержит пример кода, который отображается в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="e35f0-231">The following code contains  the sample code that appears in this topic.</span></span>

```fsharp
#if INTERACTIVE
#r "FSharp.Data.TypeProviders.dll"
#r "System.Data.dll"
#r "System.Data.Linq.dll"
#endif
open System
open Microsoft.FSharp.Data.TypeProviders
open System.Data.Linq.SqlClient
open System.Linq

type schema = SqlDataConnection<"Data Source=SERVER\INSTANCE;Initial Catalog=MyDatabase;Integrated Security=SSPI;">

let db = schema.GetDataContext()

let data = [1; 5; 7; 11; 18; 21]

type Nullable<'T when 'T : ( new : unit -> 'T) and 'T : struct and 'T :> ValueType > with
    member this.Print() =
        if this.HasValue then this.Value.ToString()
        else "NULL"

printfn "\ncontains query operator"
query {
    for student in db.Student do
    select student.Age.Value
    contains 11
}
|> printfn "Is at least one student age 11? %b"

printfn "\ncount query operator"
query {
    for student in db.Student do
    select student
    count
}
|> printfn "Number of students: %d"

printfn "\nlast query operator."
let num =
    query {
        for number in data do
        sortBy number
        last
    }
printfn "Last number: %d" num


open Microsoft.FSharp.Linq

printfn "\nlastOrDefault query operator."
query {
    for number in data do
    sortBy number
    lastOrDefault
}
|> printfn "lastOrDefault: %d"

printfn "\nexactlyOne query operator."
let student2 =
    query {
        for student in db.Student do
        where (student.StudentID = 1)
        select student
        exactlyOne
    }
printfn "Student with StudentID = 1 is %s" student2.Name

printfn "\nexactlyOneOrDefault query operator."
let student3 =
    query {
        for student in db.Student do
        where (student.StudentID = 1)
        select student
        exactlyOneOrDefault
    }
printfn "Student with StudentID = 1 is %s" student3.Name

printfn "\nheadOrDefault query operator."
let student4 =
    query {
        for student in db.Student do
        select student
        headOrDefault
    }
printfn "head student is %s" student4.Name

printfn "\nselect query operator."
query {
    for student in db.Student do
    select student
}
|> Seq.iter (fun student -> printfn "StudentID, Name: %d %s" student.StudentID student.Name)

printfn "\nwhere query operator."
query {
    for student in db.Student do
    where (student.StudentID > 4)
    select student
}
|> Seq.iter (fun student -> printfn "StudentID, Name: %d %s" student.StudentID student.Name)

printfn "\nminBy query operator."
let student5 =
    query {
        for student in db.Student do
        minBy student.StudentID
    }

printfn "\nmaxBy query operator."
let student6 =
    query {
        for student in db.Student do
        maxBy student.StudentID
    }

printfn "\ngroupBy query operator."
query {
    for student in db.Student do
    groupBy student.Age into g
    select (g.Key, g.Count())
}
|> Seq.iter (fun (age, count) -> printfn "Age: %s Count at that age: %d" (age.Print()) count)

printfn "\nsortBy query operator."
query {
    for student in db.Student do
    sortBy student.Name
    select student
}
|> Seq.iter (fun student -> printfn "StudentID, Name: %d %s" student.StudentID student.Name)

printfn "\nsortByDescending query operator."
query {
    for student in db.Student do
    sortByDescending student.Name
    select student
}
|> Seq.iter (fun student -> printfn "StudentID, Name: %d %s" student.StudentID student.Name)

printfn "\nthenBy query operator."
query {
    for student in db.Student do
    where student.Age.HasValue
    sortBy student.Age.Value
    thenBy student.Name
    select student
}
|> Seq.iter (fun student -> printfn "StudentID, Name: %d %s" student.Age.Value student.Name)

printfn "\nthenByDescending query operator."
query {
    for student in db.Student do
    where student.Age.HasValue
    sortBy student.Age.Value
    thenByDescending student.Name
    select student
}
|> Seq.iter (fun student -> printfn "StudentID, Name: %d %s" student.Age.Value student.Name)

printfn "\ngroupValBy query operator."
query {
    for student in db.Student do
    groupValBy student.Name student.Age into g
    select (g, g.Key, g.Count())
}
|> Seq.iter (fun (group, age, count) ->
    printfn "Age: %s Count at that age: %d" (age.Print()) count
    group |> Seq.iter (fun name -> printfn "Name: %s" name))

printfn "\n sumByNullable query operator"
query {
    for student in db.Student do
    sumByNullable student.Age
}
|> (fun sum -> printfn "Sum of ages: %s" (sum.Print()))

printfn "\n minByNullable"
query {
    for student in db.Student do
    minByNullable student.Age
}
|> (fun age -> printfn "Minimum age: %s" (age.Print()))

printfn "\n maxByNullable"
query {
    for student in db.Student do
    maxByNullable student.Age
}
|> (fun age -> printfn "Maximum age: %s" (age.Print()))

printfn "\n averageBy"
query {
    for student in db.Student do
    averageBy (float student.StudentID)
}
|> printfn "Average student ID: %f"

printfn "\n averageByNullable"
query {
    for student in db.Student do
    averageByNullable (Nullable.float student.Age)
}
|> (fun avg -> printfn "Average age: %s" (avg.Print()))

printfn "\n find query operator"
query {
    for student in db.Student do
    find (student.Name = "Abercrombie, Kim")
}
|> (fun student -> printfn "Found a match with StudentID = %d" student.StudentID)

printfn "\n all query operator"
query {
    for student in db.Student do
    all (SqlMethods.Like(student.Name, "%,%"))
}
|> printfn "Do all students have a comma in the name? %b"

printfn "\n head query operator"
query {
    for student in db.Student do
    head
}
|> (fun student -> printfn "Found the head student with StudentID = %d" student.StudentID)

printfn "\n nth query operator"
query {
    for numbers in data do
    nth 3
}
|> printfn "Third number is %d"

printfn "\n skip query operator"
query {
    for student in db.Student do
    skip 1
}
|> Seq.iter (fun student -> printfn "StudentID = %d" student.StudentID)

printfn "\n skipWhile query operator"
query {
    for number in data do
    skipWhile (number < 3)
    select number
}
|> Seq.iter (fun number -> printfn "Number = %d" number)


printfn "\n sumBy query operator"
query {
    for student in db.Student do
    sumBy student.StudentID
}
|> printfn "Sum of student IDs: %d"

printfn "\n take query operator"
query {
    for student in db.Student do
    select student
    take 2
}
|> Seq.iter (fun student -> printfn "StudentID = %d" student.StudentID)

printfn "\n takeWhile query operator"
query {
    for number in data do
    takeWhile (number < 10)
}
|> Seq.iter (fun number -> printfn "Number = %d" number)

printfn "\n sortByNullable query operator"
query {
    for student in db.Student do
    sortByNullable student.Age
    select student
}
|> Seq.iter (fun student ->
    printfn "StudentID, Name, Age: %d %s %s" student.StudentID student.Name (student.Age.Print()))

printfn "\n sortByNullableDescending query operator"
query {
    for student in db.Student do
    sortByNullableDescending student.Age
    select student
}
|> Seq.iter (fun student ->
    printfn "StudentID, Name, Age: %d %s %s" student.StudentID student.Name (student.Age.Print()))

printfn "\n thenByNullable query operator"
query {
    for student in db.Student do
    sortBy student.Name
    thenByNullable student.Age
    select student
}
|> Seq.iter (fun student ->
    printfn "StudentID, Name, Age: %d %s %s" student.StudentID student.Name (student.Age.Print()))

printfn "\n thenByNullableDescending query operator"
query {
    for student in db.Student do
    sortBy student.Name
    thenByNullableDescending student.Age
    select student
}
|> Seq.iter (fun student ->
    printfn "StudentID, Name, Age: %d %s %s" student.StudentID student.Name (student.Age.Print()))

printfn "All students: "
query {
    for student in db.Student do
    select student
}
|> Seq.iter (fun student -> printfn "%s %d %s" student.Name student.StudentID (student.Age.Print()))

printfn "\nCount of students: "
query {
    for student in db.Student do
    count
}
|> (fun count -> printfn "Student count: %d" count)

printfn "\nExists."
query {
    for student in db.Student do
    where
        (query {
            for courseSelection in db.CourseSelection do
            exists (courseSelection.StudentID = student.StudentID) })
    select student
}
|> Seq.iter (fun student -> printfn "%A" student.Name)

printfn "\n Group by age and count"
query {
    for n in db.Student do
    groupBy n.Age into g
    select (g.Key, g.Count())
}
|> Seq.iter (fun (age, count) -> printfn "%s %d" (age.Print()) count)

printfn "\n Group value by age."
query {
    for n in db.Student do
    groupValBy n.Age n.Age into g
    select (g.Key, g.Count())
}
|> Seq.iter (fun (age, count) -> printfn "%s %d" (age.Print()) count)

printfn "\nGroup students by age where age > 10."
query {
    for student in db.Student do
    groupBy student.Age into g
    where (g.Key.HasValue && g.Key.Value > 10)
    select (g, g.Key)
}
|> Seq.iter (fun (students, age) ->
    printfn "Age: %s" (age.Value.ToString())
    students
    |> Seq.iter (fun student -> printfn "%s" student.Name))

printfn "\nGroup students by age and print counts of number of students at each age with more than 1 student."
query {
    for student in db.Student do
    groupBy student.Age into group
    where (group.Count() > 1)
    select (group.Key, group.Count())
}
|> Seq.iter (fun (age, ageCount) ->
    printfn "Age: %s Count: %d" (age.Print()) ageCount)

printfn "\nGroup students by age and sum ages."
query {
    for student in db.Student do
    groupBy student.Age into g
    let total = query { for student in g do sumByNullable student.Age }
    select (g.Key, g.Count(), total)
}
|> Seq.iter (fun (age, count, total) ->
    printfn "Age: %d" (age.GetValueOrDefault())
    printfn "Count: %d" count
    printfn "Total years: %s" (total.ToString()))

printfn "\nGroup students by age and count number of students at each age, and display all with count > 1 in descending order of count."
query {
    for student in db.Student do
    groupBy student.Age into g
    where (g.Count() > 1)
    sortByDescending (g.Count())
    select (g.Key, g.Count())
}
|> Seq.iter (fun (age, myCount) ->
    printfn "Age: %s" (age.Print())
    printfn "Count: %d" myCount)

printfn "\n Select students from a set of IDs"
let idList = [1; 2; 5; 10]
let idQuery =
    query { for id in idList do select id }
query {
    for student in db.Student do
    where (idQuery.Contains(student.StudentID))
    select student
}
|> Seq.iter (fun student ->
    printfn "Name: %s" student.Name)

printfn "\nLook for students with Name match _e%% pattern and take first two."
query {
    for student in db.Student do
    where (SqlMethods.Like( student.Name, "_e%") )
    select student
    take 2
}
|> Seq.iter (fun student -> printfn "%s" student.Name)

printfn "\nLook for students with Name matching [abc]%% pattern."
query {
    for student in db.Student do
    where (SqlMethods.Like( student.Name, "[abc]%") )
    select student
}
|> Seq.iter (fun student -> printfn "%s" student.Name)

printfn "\nLook for students with name matching [^abc]%% pattern."
query {
    for student in db.Student do
    where (SqlMethods.Like( student.Name, "[^abc]%") )
    select student
}
|> Seq.iter (fun student -> printfn "%s" student.Name)

printfn "\nLook for students with name matching [^abc]%% pattern and select ID."
query {
    for n in db.Student do
    where (SqlMethods.Like( n.Name, "[^abc]%") )
    select n.StudentID
}
|> Seq.iter (fun id -> printfn "%d" id)

printfn "\n Using Contains as a query filter."
query {
    for student in db.Student do
    where (student.Name.Contains("a"))
    select student
}
|> Seq.iter (fun student -> printfn "%s" student.Name)

printfn "\nSearching for names from a list."
let names = [|"a";"b";"c"|]
query {
    for student in db.Student do
    if names.Contains (student.Name) then select student
}
|> Seq.iter (fun student -> printfn "%s" student.Name)

printfn "\nJoin Student and CourseSelection tables."
query {
    for student in db.Student do
    join selection in db.CourseSelection
        on (student.StudentID = selection.StudentID)
    select (student, selection)
}
|> Seq.iter (fun (student, selection) -> printfn "%d %s %d" student.StudentID student.Name selection.CourseID)

printfn "\nLeft Join Student and CourseSelection tables."
query {
    for student in db.Student do
    leftOuterJoin selection in db.CourseSelection
        on (student.StudentID = selection.StudentID) into result
    for selection in result.DefaultIfEmpty() do
    select (student, selection)
}
|> Seq.iter (fun (student, selection) ->
    let selectionID, studentID, courseID =
        match selection with
        | null -> "NULL", "NULL", "NULL"
        | sel -> (sel.ID.ToString(), sel.StudentID.ToString(), sel.CourseID.ToString())
    printfn "%d %s %d %s %s %s" student.StudentID student.Name (student.Age.GetValueOrDefault()) selectionID studentID courseID)

printfn "\nJoin with count"
query {
    for n in db.Student do
    join e in db.CourseSelection
        on (n.StudentID = e.StudentID)
    count
}
|> printfn "%d"

printfn "\n Join with distinct."
query {
    for student in db.Student do
    join selection in db.CourseSelection
        on (student.StudentID = selection.StudentID)
    distinct
}
|> Seq.iter (fun (student, selection) -> printfn "%s %d" student.Name selection.CourseID)

printfn "\n Join with distinct and count."
query {
    for n in db.Student do
    join e in db.CourseSelection
        on (n.StudentID = e.StudentID)
    distinct
    count
}
|> printfn "%d"

printfn "\n Selecting students with age between 10 and 15."
query {
    for student in db.Student do
    where (student.Age.Value >= 10 && student.Age.Value < 15)
    select student
}
|> Seq.iter (fun student -> printfn "%s" student.Name)

printfn "\n Selecting students with age either 11 or 12."
query {
    for student in db.Student do
    where (student.Age.Value = 11 || student.Age.Value = 12)
    select student
}
|> Seq.iter (fun student -> printfn "%s" student.Name)

printfn "\n Selecting students in a certain age range and sorting."
query {
    for n in db.Student do
    where (n.Age.Value = 12 || n.Age.Value = 13)
    sortByNullableDescending n.Age
    select n
}
|> Seq.iter (fun student -> printfn "%s %s" student.Name (student.Age.Print()))

printfn "\n Selecting students with certain ages, taking account of possibility of nulls."
query {
    for student in db.Student do
    where
        ((student.Age.HasValue && student.Age.Value = 11) ||
         (student.Age.HasValue && student.Age.Value = 12))
    sortByDescending student.Name
    select student.Name
    take 2
}
|> Seq.iter (fun name -> printfn "%s" name)

printfn "\n Union of two queries."
module Queries =
    let query1 = query {
        for n in db.Student do
        select (n.Name, n.Age)
    }

    let query2 = query {
        for n in db.LastStudent do
        select (n.Name, n.Age)
    }

    query2.Union (query1)
    |> Seq.iter (fun (name, age) -> printfn "%s %s" name (age.Print()))

printfn "\n Intersect of two queries."
module Queries2 =
    let query1 = query {
        for n in db.Student do
        select (n.Name, n.Age)
    }

    let query2 = query {
        for n in db.LastStudent do
        select (n.Name, n.Age)
    }

    query1.Intersect(query2)
    |> Seq.iter (fun (name, age) -> printfn "%s %s" name (age.Print()))

printfn "\n Using if statement to alter results for special value."
query {
    for student in db.Student do
    select
        (if student.Age.HasValue && student.Age.Value = -1 then
            (student.StudentID, System.Nullable<int>(100), student.Age)
         else (student.StudentID, student.Age, student.Age))
}
|> Seq.iter (fun (id, value, age) -> printfn "%d %s %s" id (value.Print()) (age.Print()))

printfn "\n Using if statement to alter results special values."
query {
    for student in db.Student do
    select
        (if student.Age.HasValue && student.Age.Value = -1 then
            (student.StudentID, System.Nullable<int>(100), student.Age)
         elif student.Age.HasValue && student.Age.Value = 0 then
            (student.StudentID, System.Nullable<int>(100), student.Age)
         else (student.StudentID, student.Age, student.Age))
}
|> Seq.iter (fun (id, value, age) -> printfn "%d %s %s" id (value.Print()) (age.Print()))

printfn "\n Multiple table select."
query {
    for student in db.Student do
    for course in db.Course do
    select (student, course)
}
|> Seq.iteri (fun index (student, course) ->
    if index = 0 then
        printfn "StudentID Name Age CourseID CourseName"
    printfn "%d %s %s %d %s" student.StudentID student.Name (student.Age.Print()) course.CourseID course.CourseName)

printfn "\nMultiple Joins"
query {
    for student in db.Student do
    join courseSelection in db.CourseSelection
        on (student.StudentID = courseSelection.StudentID)
    join course in db.Course
        on (courseSelection.CourseID = course.CourseID)
    select (student.Name, course.CourseName)
}
|> Seq.iter (fun (studentName, courseName) -> printfn "%s %s" studentName courseName)

printfn "\nMultiple Left Outer Joins"
query {
    for student in db.Student do
    leftOuterJoin courseSelection in db.CourseSelection
        on (student.StudentID = courseSelection.StudentID) into g1
    for courseSelection in g1.DefaultIfEmpty() do
    leftOuterJoin course in db.Course
        on (courseSelection.CourseID = course.CourseID) into g2
    for course in g2.DefaultIfEmpty() do
    select (student.Name, course.CourseName)
}
|> Seq.iter (fun (studentName, courseName) -> printfn "%s %s" studentName courseName)
```

<span data-ttu-id="e35f0-232">А вот полные результаты при выполнении этого кода в F # Interactive.</span><span class="sxs-lookup"><span data-stu-id="e35f0-232">And here is the full output when this code is run in F# Interactive.</span></span>

```
--> Referenced 'C:\Program Files (x86)\Reference Assemblies\Microsoft\FSharp\3.0\Runtime\v4.0\Type Providers\FSharp.Data.TypeProviders.dll'


--> Referenced 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\System.Data.dll'


--> Referenced 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\System.Data.Linq.dll'


contains query operator
Binding session to 'C:\Users\ghogen\AppData\Local\Temp\tmp5E3C.dll'...
Binding session to 'C:\Users\ghogen\AppData\Local\Temp\tmp611A.dll'...
Is at least one student age 11? true

count query operator
Number of students: 8

last query operator.
Last number: 21

lastOrDefault query operator.
lastOrDefault: 21

exactlyOne query operator.
Student with StudentID = 1 is Abercrombie, Kim

exactlyOneOrDefault query operator.
Student with StudentID = 1 is Abercrombie, Kim

headOrDefault query operator.
head student is Abercrombie, Kim

select query operator.
StudentID, Name: 1 Abercrombie, Kim
StudentID, Name: 2 Abolrous, Hazen
StudentID, Name: 3 Hance, Jim
StudentID, Name: 4 Adams, Terry
StudentID, Name: 5 Hansen, Claus
StudentID, Name: 6 Penor, Lori
StudentID, Name: 7 Perham, Tom
StudentID, Name: 8 Peng, Yun-Feng

where query operator.
StudentID, Name: 5 Hansen, Claus
StudentID, Name: 6 Penor, Lori
StudentID, Name: 7 Perham, Tom
StudentID, Name: 8 Peng, Yun-Feng

minBy query operator.

maxBy query operator.

groupBy query operator.
Age: NULL Count at that age: 1
Age: 10 Count at that age: 1
Age: 11 Count at that age: 1
Age: 12 Count at that age: 3
Age: 13 Count at that age: 1
Age: 14 Count at that age: 1

sortBy query operator.
StudentID, Name: 1 Abercrombie, Kim
StudentID, Name: 2 Abolrous, Hazen
StudentID, Name: 4 Adams, Terry
StudentID, Name: 3 Hance, Jim
StudentID, Name: 5 Hansen, Claus
StudentID, Name: 8 Peng, Yun-Feng
StudentID, Name: 6 Penor, Lori
StudentID, Name: 7 Perham, Tom

sortByDescending query operator.
StudentID, Name: 7 Perham, Tom
StudentID, Name: 6 Penor, Lori
StudentID, Name: 8 Peng, Yun-Feng
StudentID, Name: 5 Hansen, Claus
StudentID, Name: 3 Hance, Jim
StudentID, Name: 4 Adams, Terry
StudentID, Name: 2 Abolrous, Hazen
StudentID, Name: 1 Abercrombie, Kim

thenBy query operator.
StudentID, Name: 10 Abercrombie, Kim
StudentID, Name: 11 Hansen, Claus
StudentID, Name: 12 Adams, Terry
StudentID, Name: 12 Hance, Jim
StudentID, Name: 12 Perham, Tom
StudentID, Name: 13 Penor, Lori
StudentID, Name: 14 Abolrous, Hazen

thenByDescending query operator.
StudentID, Name: 10 Abercrombie, Kim
StudentID, Name: 11 Hansen, Claus
StudentID, Name: 12 Perham, Tom
StudentID, Name: 12 Hance, Jim
StudentID, Name: 12 Adams, Terry
StudentID, Name: 13 Penor, Lori
StudentID, Name: 14 Abolrous, Hazen

groupValBy query operator.
Age: NULL Count at that age: 1
Name: Peng, Yun-Feng
Age: 10 Count at that age: 1
Name: Abercrombie, Kim
Age: 11 Count at that age: 1
Name: Hansen, Claus
Age: 12 Count at that age: 3
Name: Hance, Jim
Name: Adams, Terry
Name: Perham, Tom
Age: 13 Count at that age: 1
Name: Penor, Lori
Age: 14 Count at that age: 1
Name: Abolrous, Hazen

sumByNullable query operator
Sum of ages: 84

minByNullable
Minimum age: 10

maxByNullable
Maximum age: 14

averageBy
Average student ID: 4.500000

averageByNullable
Average age: 12

find query operator
Found a match with StudentID = 1

all query operator
Do all students have a comma in the name? true

head query operator
Found the head student with StudentID = 1

nth query operator
Third number is 11

skip query operator
StudentID = 2
StudentID = 3
StudentID = 4
StudentID = 5
StudentID = 6
StudentID = 7
StudentID = 8

skipWhile query operator
Number = 5
Number = 7
Number = 11
Number = 18
Number = 21

sumBy query operator
Sum of student IDs: 36

take query operator
StudentID = 1
StudentID = 2

takeWhile query operator
Number = 1
Number = 5
Number = 7

sortByNullable query operator
StudentID, Name, Age: 8 Peng, Yun-Feng NULL
StudentID, Name, Age: 1 Abercrombie, Kim 10
StudentID, Name, Age: 5 Hansen, Claus 11
StudentID, Name, Age: 7 Perham, Tom 12
StudentID, Name, Age: 3 Hance, Jim 12
StudentID, Name, Age: 4 Adams, Terry 12
StudentID, Name, Age: 6 Penor, Lori 13
StudentID, Name, Age: 2 Abolrous, Hazen 14

sortByNullableDescending query operator
StudentID, Name, Age: 2 Abolrous, Hazen 14
StudentID, Name, Age: 6 Penor, Lori 13
StudentID, Name, Age: 7 Perham, Tom 12
StudentID, Name, Age: 3 Hance, Jim 12
StudentID, Name, Age: 4 Adams, Terry 12
StudentID, Name, Age: 5 Hansen, Claus 11
StudentID, Name, Age: 1 Abercrombie, Kim 10
StudentID, Name, Age: 8 Peng, Yun-Feng NULL

thenByNullable query operator
StudentID, Name, Age: 1 Abercrombie, Kim 10
StudentID, Name, Age: 2 Abolrous, Hazen 14
StudentID, Name, Age: 4 Adams, Terry 12
StudentID, Name, Age: 3 Hance, Jim 12
StudentID, Name, Age: 5 Hansen, Claus 11
StudentID, Name, Age: 8 Peng, Yun-Feng NULL
StudentID, Name, Age: 6 Penor, Lori 13
StudentID, Name, Age: 7 Perham, Tom 12

thenByNullableDescending query operator
StudentID, Name, Age: 1 Abercrombie, Kim 10
StudentID, Name, Age: 2 Abolrous, Hazen 14
StudentID, Name, Age: 4 Adams, Terry 12
StudentID, Name, Age: 3 Hance, Jim 12
StudentID, Name, Age: 5 Hansen, Claus 11
StudentID, Name, Age: 8 Peng, Yun-Feng NULL
StudentID, Name, Age: 6 Penor, Lori 13
StudentID, Name, Age: 7 Perham, Tom 12
All students:
Abercrombie, Kim 1 10
Abolrous, Hazen 2 14
Hance, Jim 3 12
Adams, Terry 4 12
Hansen, Claus 5 11
Penor, Lori 6 13
Perham, Tom 7 12
Peng, Yun-Feng 8 NULL

Count of students:
Student count: 8

Exists.
"Abercrombie, Kim"
"Abolrous, Hazen"
"Hance, Jim"
"Adams, Terry"
"Hansen, Claus"
"Perham, Tom"

Group by age and count
NULL 1
10 1
11 1
12 3
13 1
14 1

Group value by age.
NULL 1
10 1
11 1
12 3
13 1
14 1

Group students by age where age > 10.
Age: 11
Hansen, Claus
Age: 12
Hance, Jim
Adams, Terry
Perham, Tom
Age: 13
Penor, Lori
Age: 14
Abolrous, Hazen

Group students by age and print counts of number of students at each age with more than 1 student.
Age: 12 Count: 3

Group students by age and sum ages.
Age: 0
Count: 1
Total years:
Age: 10
Count: 1
Total years: 10
Age: 11
Count: 1
Total years: 11
Age: 12
Count: 3
Total years: 36
Age: 13
Count: 1
Total years: 13
Age: 14
Count: 1
Total years: 14

Group students by age and count number of students at each age, and display all with count > 1 in descending order of count.
Age: 12
Count: 3

Select students from a set of IDs
Name: Abercrombie, Kim
Name: Abolrous, Hazen
Name: Hansen, Claus

Look for students with Name match _e% pattern and take first two.
Penor, Lori
Perham, Tom

Look for students with Name matching [abc]% pattern.
Abercrombie, Kim
Abolrous, Hazen
Adams, Terry

Look for students with name matching [^abc]% pattern.
Hance, Jim
Hansen, Claus
Penor, Lori
Perham, Tom
Peng, Yun-Feng

Look for students with name matching [^abc]% pattern and select ID.
3
5
6
7
8

Using Contains as a query filter.
Abercrombie, Kim
Abolrous, Hazen
Hance, Jim
Adams, Terry
Hansen, Claus
Perham, Tom

Searching for names from a list.

Join Student and CourseSelection tables.
2 Abolrous, Hazen 2
3 Hance, Jim 3
5 Hansen, Claus 5
2 Abolrous, Hazen 2
5 Hansen, Claus 5
6 Penor, Lori 6
3 Hance, Jim 3
2 Abolrous, Hazen 2
1 Abercrombie, Kim 1
2 Abolrous, Hazen 2
5 Hansen, Claus 5
2 Abolrous, Hazen 2
3 Hance, Jim 3
2 Abolrous, Hazen 2
3 Hance, Jim 3

Left Join Student and CourseSelection tables.
1 Abercrombie, Kim 10 9 3 1
2 Abolrous, Hazen 14 1 1 2
2 Abolrous, Hazen 14 4 2 2
2 Abolrous, Hazen 14 8 3 2
2 Abolrous, Hazen 14 10 4 2
2 Abolrous, Hazen 14 12 4 2
2 Abolrous, Hazen 14 14 5 2
3 Hance, Jim 12 2 1 3
3 Hance, Jim 12 7 2 3
3 Hance, Jim 12 13 5 3
3 Hance, Jim 12 15 7 3
4 Adams, Terry 12 NULL NULL NULL
5 Hansen, Claus 11 3 1 5
5 Hansen, Claus 11 5 2 5
5 Hansen, Claus 11 11 4 5
6 Penor, Lori 13 6 2 6
7 Perham, Tom 12 NULL NULL NULL
8 Peng, Yun-Feng 0 NULL NULL NULL

Join with count
15

Join with distinct.
Abercrombie, Kim 2
Abercrombie, Kim 3
Abercrombie, Kim 5
Abolrous, Hazen 2
Abolrous, Hazen 5
Abolrous, Hazen 6
Abolrous, Hazen 3
Hance, Jim 2
Hance, Jim 1
Adams, Terry 2
Adams, Terry 5
Adams, Terry 2
Hansen, Claus 3
Hansen, Claus 2
Perham, Tom 3

Join with distinct and count.
15

Selecting students with age between 10 and 15.
Abercrombie, Kim
Abolrous, Hazen
Hance, Jim
Adams, Terry
Hansen, Claus
Penor, Lori
Perham, Tom

Selecting students with age either 11 or 12.
Hance, Jim
Adams, Terry
Hansen, Claus
Perham, Tom

Selecting students in a certain age range and sorting.
Penor, Lori 13
Perham, Tom 12
Hance, Jim 12
Adams, Terry 12

Selecting students with certain ages, taking account of possibility of nulls.
Hance, Jim
Adams, Terry

Union of two queries.
Abercrombie, Kim 10
Abolrous, Hazen 14
Hance, Jim 12
Adams, Terry 12
Hansen, Claus 11
Penor, Lori 13
Perham, Tom 12
Peng, Yun-Feng NULL

Intersect of two queries.

Using if statement to alter results for special value.
1 10 10
2 14 14
3 12 12
4 12 12
5 11 11
6 13 13
7 12 12
8 NULL NULL

Using if statement to alter results special values.
1 10 10
2 14 14
3 12 12
4 12 12
5 11 11
6 13 13
7 12 12
8 NULL NULL

Multiple table select.
StudentID Name Age CourseID CourseName
1 Abercrombie, Kim 10 1 Algebra I
2 Abolrous, Hazen 14 1 Algebra I
3 Hance, Jim 12 1 Algebra I
4 Adams, Terry 12 1 Algebra I
5 Hansen, Claus 11 1 Algebra I
6 Penor, Lori 13 1 Algebra I
7 Perham, Tom 12 1 Algebra I
8 Peng, Yun-Feng NULL 1 Algebra I
1 Abercrombie, Kim 10 2 Trigonometry
2 Abolrous, Hazen 14 2 Trigonometry
3 Hance, Jim 12 2 Trigonometry
4 Adams, Terry 12 2 Trigonometry
5 Hansen, Claus 11 2 Trigonometry
6 Penor, Lori 13 2 Trigonometry
7 Perham, Tom 12 2 Trigonometry
8 Peng, Yun-Feng NULL 2 Trigonometry
1 Abercrombie, Kim 10 3 Algebra II
2 Abolrous, Hazen 14 3 Algebra II
3 Hance, Jim 12 3 Algebra II
4 Adams, Terry 12 3 Algebra II
5 Hansen, Claus 11 3 Algebra II
6 Penor, Lori 13 3 Algebra II
7 Perham, Tom 12 3 Algebra II
8 Peng, Yun-Feng NULL 3 Algebra II
1 Abercrombie, Kim 10 4 History
2 Abolrous, Hazen 14 4 History
3 Hance, Jim 12 4 History
4 Adams, Terry 12 4 History
5 Hansen, Claus 11 4 History
6 Penor, Lori 13 4 History
7 Perham, Tom 12 4 History
8 Peng, Yun-Feng NULL 4 History
1 Abercrombie, Kim 10 5 English
2 Abolrous, Hazen 14 5 English
3 Hance, Jim 12 5 English
4 Adams, Terry 12 5 English
5 Hansen, Claus 11 5 English
6 Penor, Lori 13 5 English
7 Perham, Tom 12 5 English
8 Peng, Yun-Feng NULL 5 English
1 Abercrombie, Kim 10 6 French
2 Abolrous, Hazen 14 6 French
3 Hance, Jim 12 6 French
4 Adams, Terry 12 6 French
5 Hansen, Claus 11 6 French
6 Penor, Lori 13 6 French
7 Perham, Tom 12 6 French
8 Peng, Yun-Feng NULL 6 French
1 Abercrombie, Kim 10 7 Chinese
2 Abolrous, Hazen 14 7 Chinese
3 Hance, Jim 12 7 Chinese
4 Adams, Terry 12 7 Chinese
5 Hansen, Claus 11 7 Chinese
6 Penor, Lori 13 7 Chinese
7 Perham, Tom 12 7 Chinese
8 Peng, Yun-Feng NULL 7 Chinese

Multiple Joins
Abercrombie, Kim Trigonometry
Abercrombie, Kim Algebra II
Abercrombie, Kim English
Abolrous, Hazen Trigonometry
Abolrous, Hazen English
Abolrous, Hazen French
Abolrous, Hazen Algebra II
Hance, Jim Trigonometry
Hance, Jim Algebra I
Adams, Terry Trigonometry
Adams, Terry English
Adams, Terry Trigonometry
Hansen, Claus Algebra II
Hansen, Claus Trigonometry
Perham, Tom Algebra II

Multiple Left Outer Joins
Abercrombie, Kim Trigonometry
Abercrombie, Kim Algebra II
Abercrombie, Kim English
Abolrous, Hazen Trigonometry
Abolrous, Hazen English
Abolrous, Hazen French
Abolrous, Hazen Algebra II
Hance, Jim Trigonometry
Hance, Jim Algebra I
Adams, Terry Trigonometry
Adams, Terry English
Adams, Terry Trigonometry
Hansen, Claus Algebra II
Hansen, Claus Trigonometry
Penor, Lori
Perham, Tom Algebra II
Peng, Yun-Feng

type schema
val db : schema.ServiceTypes.SimpleDataContextTypes.MyDatabase1
val student : System.Data.Linq.Table<schema.ServiceTypes.Student>
val data : int list = [1; 5; 7; 11; 18; 21]
type Nullable<'T
                when 'T : (new : unit ->  'T) and 'T : struct and
                     'T :> System.ValueType> with
  member Print : unit -> string
val num : int = 21
val student2 : schema.ServiceTypes.Student
val student3 : schema.ServiceTypes.Student
val student4 : schema.ServiceTypes.Student
val student5 : int = 1
val student6 : int = 8
val idList : int list = [1; 2; 5; 10]
val idQuery : seq<int>
val names : string [] = [|"a"; "b"; "c"|]
module Queries = begin
  val query1 : System.Linq.IQueryable<string * System.Nullable<int>>
  val query2 : System.Linq.IQueryable<string * System.Nullable<int>>
end
module Queries2 = begin
  val query1 : System.Linq.IQueryable<string * System.Nullable<int>>
  val query2 : System.Linq.IQueryable<string * System.Nullable<int>>
end
```

## <a name="see-also"></a><span data-ttu-id="e35f0-233">См. также</span><span class="sxs-lookup"><span data-stu-id="e35f0-233">See Also</span></span>
[<span data-ttu-id="e35f0-234">Справочник по языку F#</span><span class="sxs-lookup"><span data-stu-id="e35f0-234">F# Language Reference</span></span>](index.md)

[<span data-ttu-id="e35f0-235">Класс Linq.QueryBuilder</span><span class="sxs-lookup"><span data-stu-id="e35f0-235">Linq.QueryBuilder Class</span></span>](https://msdn.microsoft.com/visualfsharpdocs/conceptual/linq.querybuilder-class-%5bfsharp%5d)

[<span data-ttu-id="e35f0-236">Выражения вычисления</span><span class="sxs-lookup"><span data-stu-id="e35f0-236">Computation Expressions</span></span>](Computation-Expressions.md)