---
title: Использование XSLT для преобразования дерева XML (C#)
ms.date: 07/20/2015
ms.assetid: 373a2699-d4c5-471b-9bda-c1f0ab73b477
ms.openlocfilehash: 3fa850c0f09404da49b2963e980d15e1ed54316f
ms.sourcegitcommit: ad99773e5e45068ce03b99518008397e1299e0d1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/22/2018
ms.locfileid: "46585950"
---
# <a name="using-xslt-to-transform-an-xml-tree-c"></a>Использование XSLT для преобразования дерева XML (C#)
Можно создавать XML-дерево, <xref:System.Xml.XmlReader> из XML-дерева, новый документ и <xref:System.Xml.XmlWriter>, который будет заносить информацию в новый документ. После этого можно вызвать преобразование XSLT, передавая <xref:System.Xml.XmlReader> и <xref:System.Xml.XmlWriter> этой трансформации. После успешного завершения преобразования новое XML-дерево заполняется ее результатами.  
  
## <a name="example"></a>Пример  
  
```csharp  
string xslMarkup = @"<?xml version='1.0'?>  
<xsl:stylesheet xmlns:xsl='http://www.w3.org/1999/XSL/Transform' version='1.0'>  
    <xsl:template match='/Parent'>  
        <Root>  
            <C1>  
            <xsl:value-of select='Child1'/>  
            </C1>  
            <C2>  
            <xsl:value-of select='Child2'/>  
            </C2>  
        </Root>  
    </xsl:template>  
</xsl:stylesheet>";  
  
XDocument xmlTree = new XDocument(  
    new XElement("Parent",  
        new XElement("Child1", "Child1 data"),  
        new XElement("Child2", "Child2 data")  
    )  
);  
  
XDocument newTree = new XDocument();  
using (XmlWriter writer = newTree.CreateWriter()) {  
    // Load the style sheet.  
    XslCompiledTransform xslt = new XslCompiledTransform();  
    xslt.Load(XmlReader.Create(new StringReader(xslMarkup)));  
  
    // Execute the transform and output the results to a writer.  
    xslt.Transform(xmlTree.CreateReader(), writer);  
}  
  
Console.WriteLine(newTree);  
```  
  
 В этом примере выводятся следующие данные:  
  
```xml  
<Root>  
  <C1>Child1 data</C1>  
  <C2>Child2 data</C2>  
</Root>  
```  
  
## <a name="see-also"></a>См. также

- <xref:System.Xml.Linq.XContainer.CreateWriter%2A?displayProperty=nameWithType>  
- <xref:System.Xml.Linq.XNode.CreateReader%2A?displayProperty=nameWithType>  
- [Расширенные методы программирования LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)
