---
title: Serializar para um XmlReader (Invoke XSLT)-LINQ to XML
description: Você pode usar CreateReader para criar um XmlReader que fornece nós de uma árvore XML para uma transformação XSLT.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 4cc3ee03-ef4c-429b-a408-fedd10b728cd
ms.openlocfilehash: e079627b5fe114438feabaa1a49f42a65afedf43
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551900"
---
# <a name="serialize-to-an-xmlreader-invoke-xslt-linq-to-xml"></a><span data-ttu-id="df944-103">Serializar para um XmlReader (Invoke XSLT) (LINQ to XML)</span><span class="sxs-lookup"><span data-stu-id="df944-103">Serialize to an XmlReader (invoke XSLT) (LINQ to XML)</span></span>

<span data-ttu-id="df944-104">Ao usar os <xref:System.Xml?displayProperty=nameWithType> recursos de interoperabilidade do LINQ to XML, você pode usar o <xref:System.Xml.Linq.XNode.CreateReader%2A> para criar um <xref:System.Xml.XmlReader> .</span><span class="sxs-lookup"><span data-stu-id="df944-104">When you use the <xref:System.Xml?displayProperty=nameWithType> interoperability capabilities of LINQ to XML, you can use <xref:System.Xml.Linq.XNode.CreateReader%2A> to create an <xref:System.Xml.XmlReader>.</span></span> <span data-ttu-id="df944-105">O módulo que lê deste <xref:System.Xml.XmlReader> lê os nós da árvore XML e processa-os de acordo.</span><span class="sxs-lookup"><span data-stu-id="df944-105">The module that reads from this <xref:System.Xml.XmlReader> reads the nodes from the XML tree and processes them accordingly.</span></span>

## <a name="example-invoke-an-xslt-transformation"></a><span data-ttu-id="df944-106">Exemplo: invocar uma transformação XSLT</span><span class="sxs-lookup"><span data-stu-id="df944-106">Example: Invoke an XSLT transformation</span></span>

<span data-ttu-id="df944-107">Um uso possível para este método é ao chamar uma transformação XSLT.</span><span class="sxs-lookup"><span data-stu-id="df944-107">One possible use for this method is when invoking an XSLT transformation.</span></span> <span data-ttu-id="df944-108">Você pode criar uma árvore XML, cria <xref:System.Xml.XmlReader> de árvore XML, cria um novo documento e em seguida, cria <xref:System.Xml.XmlWriter> para gravar no novo documento.</span><span class="sxs-lookup"><span data-stu-id="df944-108">You can create an XML tree, create an <xref:System.Xml.XmlReader> from the XML tree, create a new document, and then create an <xref:System.Xml.XmlWriter> to write into the new document.</span></span> <span data-ttu-id="df944-109">Em seguida, você pode chamar a transformação XSLT, passando <xref:System.Xml.XmlReader> e em <xref:System.Xml.XmlWriter>.</span><span class="sxs-lookup"><span data-stu-id="df944-109">Then, you can invoke the XSLT transformation, passing in <xref:System.Xml.XmlReader> and <xref:System.Xml.XmlWriter>.</span></span> <span data-ttu-id="df944-110">Depois que a transformação for concluída com êxito, a nova árvore XML será preenchida com os resultados da transformação.</span><span class="sxs-lookup"><span data-stu-id="df944-110">After the transformation successfully completes, the new XML tree is populated with the results of the transformation.</span></span>

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

    // Execute the transformation and output the results to a writer.
    xslt.Transform(xmlTree.CreateReader(), writer);
}

Console.WriteLine(newTree);
```

```vb
Dim xslMarkup As XDocument = _
    <?xml version='1.0'?>
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
    </xsl:stylesheet>

Dim xmlTree As XDocument = _
    <?xml version='1.0'?>
    <Parent>
        <Child1>Child1 data</Child1>
        <Child2>Child2 data</Child2>
    </Parent>

Dim newTree As XDocument = New XDocument()
Using writer As XmlWriter = newTree.CreateWriter()
    ' Load the style sheet.
    Dim xslt As XslCompiledTransform = New XslCompiledTransform()
    xslt.Load(xslMarkup.CreateReader())

    ' Execute the transformation and output the results to a writer.
    xslt.Transform(xmlTree.CreateReader(), writer)
End Using

Console.WriteLine(newTree)
```

<span data-ttu-id="df944-111">Esse exemplo gera a saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="df944-111">This example produces the following output:</span></span>

```xml
<Root>
  <C1>Child1 data</C1>
  <C2>Child2 data</C2>
</Root>
```