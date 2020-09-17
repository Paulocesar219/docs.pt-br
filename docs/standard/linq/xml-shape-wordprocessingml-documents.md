---
title: A forma XML de documentos WordprocessingML-LINQ to XML
description: Saiba mais sobre a forma XML de um documento do WordprocessingML.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 3791b5e0-c502-469b-bb75-a7bf6fdd0a94
ms.openlocfilehash: 1f5b8098923a56b638598516ed9640a28a90198a
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90551881"
---
# <a name="the-xml-shape-of-wordprocessingml-documents-linq-to-xml"></a><span data-ttu-id="e6eab-103">A forma XML de documentos WordprocessingML (LINQ to XML)</span><span class="sxs-lookup"><span data-stu-id="e6eab-103">The XML shape of WordprocessingML documents (LINQ to XML)</span></span>

<span data-ttu-id="e6eab-104">Este artigo apresenta a forma XML de um documento do WordprocessingML.</span><span class="sxs-lookup"><span data-stu-id="e6eab-104">This article introduces the XML shape of a WordprocessingML document.</span></span>

## <a name="microsoft-office-formats"></a><span data-ttu-id="e6eab-105">Formatos de Microsoft Office</span><span class="sxs-lookup"><span data-stu-id="e6eab-105">Microsoft Office formats</span></span>

<span data-ttu-id="e6eab-106">O formato de arquivo nativo para o sistema do Microsoft Office 2007 é Office Open XML (geralmente chamado de Open XML).</span><span class="sxs-lookup"><span data-stu-id="e6eab-106">The native file format for the 2007 Microsoft Office system is Office Open XML (commonly called Open XML).</span></span> <span data-ttu-id="e6eab-107">O Open XML é um formato baseado em XML que é um padrão ECMA e, no momento, está passando pelo processo de padrões ISO-IEC.</span><span class="sxs-lookup"><span data-stu-id="e6eab-107">Open XML is an XML-based format that's an Ecma standard and is currently going through the ISO-IEC standards process.</span></span> <span data-ttu-id="e6eab-108">A linguagem de marcação para arquivos de processamento de texto dentro do Open XML é chamada de WordprocessingML.</span><span class="sxs-lookup"><span data-stu-id="e6eab-108">The markup language for word processing files within Open XML is called WordprocessingML.</span></span> <span data-ttu-id="e6eab-109">Este tutorial usa arquivos de origem do WordprocessingML como entrada para os exemplos.</span><span class="sxs-lookup"><span data-stu-id="e6eab-109">This tutorial uses WordprocessingML source files as input for the examples.</span></span>

<span data-ttu-id="e6eab-110">Se você estiver usando Microsoft Office 2003, poderá salvar documentos no formato XML aberto do Office se tiver instalado o pacote de compatibilidade Microsoft Office para formatos de arquivo do Word, Excel e PowerPoint 2007.</span><span class="sxs-lookup"><span data-stu-id="e6eab-110">If you're using Microsoft Office 2003, you can save documents in the Office Open XML format if you've installed the Microsoft Office Compatibility Pack for Word, Excel, and PowerPoint 2007 File Formats.</span></span>

## <a name="the-shape-of-wordprocessingml-documents"></a><span data-ttu-id="e6eab-111">A forma de documentos do WordprocessingML</span><span class="sxs-lookup"><span data-stu-id="e6eab-111">The shape of WordprocessingML documents</span></span>

<span data-ttu-id="e6eab-112">A primeira coisa a entender é a forma XML de documentos do WordprocessingML.</span><span class="sxs-lookup"><span data-stu-id="e6eab-112">The first thing to understand is the XML shape of WordprocessingML documents.</span></span> <span data-ttu-id="e6eab-113">Um documento de WordprocessingML contém um elemento do corpo (chamado `w:body`) que contém os parágrafos do documento.</span><span class="sxs-lookup"><span data-stu-id="e6eab-113">A WordprocessingML document contains a body element (named `w:body`) that contains the paragraphs of the document.</span></span> <span data-ttu-id="e6eab-114">Cada parágrafo contém uma ou mais execuções de texto (chamado `w:r`).</span><span class="sxs-lookup"><span data-stu-id="e6eab-114">Each paragraph contains one or more text runs (named `w:r`).</span></span> <span data-ttu-id="e6eab-115">Cada execução de texto contém uma ou mais partes de texto (chamado `w:t`).</span><span class="sxs-lookup"><span data-stu-id="e6eab-115">Each text run contains one or more text pieces (named `w:t`).</span></span>

<span data-ttu-id="e6eab-116">Veja a seguir um documento muito simples de WordprocessingML:</span><span class="sxs-lookup"><span data-stu-id="e6eab-116">The following is a very simple WordprocessingML document:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<w:document
xmlns:ve="http://schemas.openxmlformats.org/markup-compatibility/2006"
xmlns:o="urn:schemas-microsoft-com:office:office"
xmlns:r="http://schemas.openxmlformats.org/officeDocument/2006/relationships"
xmlns:m="http://schemas.openxmlformats.org/officeDocument/2006/math"
xmlns:v="urn:schemas-microsoft-com:vml"
xmlns:wp="http://schemas.openxmlformats.org/drawingml/2006/wordprocessingDrawing"
xmlns:w10="urn:schemas-microsoft-com:office:word"
xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main"
xmlns:wne="http://schemas.microsoft.com/office/word/2006/wordml">
  <w:body>
    <w:p w:rsidR="00E22EB6"
         w:rsidRDefault="00E22EB6">
      <w:r>
        <w:t>This is a paragraph.</w:t>
      </w:r>
    </w:p>
    <w:p w:rsidR="00E22EB6"
         w:rsidRDefault="00E22EB6">
      <w:r>
        <w:t>This is another paragraph.</w:t>
      </w:r>
    </w:p>
  </w:body>
</w:document>
```

<span data-ttu-id="e6eab-117">Este documento contém dois parágrafos.</span><span class="sxs-lookup"><span data-stu-id="e6eab-117">This document contains two paragraphs.</span></span> <span data-ttu-id="e6eab-118">Ambos contêm uma única execução de texto, e cada execução de texto contém uma única parte de texto.</span><span class="sxs-lookup"><span data-stu-id="e6eab-118">They both contain a single text run, and each text run contains a single text piece.</span></span>

<span data-ttu-id="e6eab-119">A maneira mais fácil para ver o conteúdo de um documento de WordprocessingML no formato XML é criar um usando Microsoft Word, salvá-lo e executar o seguinte programa que lê XML no console.</span><span class="sxs-lookup"><span data-stu-id="e6eab-119">The easiest way to see the contents of a WordprocessingML document in XML form is to create one using Microsoft Word, save it, and then run the following program that prints the XML to the console.</span></span>

<span data-ttu-id="e6eab-120">Este exemplo usa as classes encontradas no assembly WindowsBase.</span><span class="sxs-lookup"><span data-stu-id="e6eab-120">This example uses classes found in the WindowsBase assembly.</span></span> <span data-ttu-id="e6eab-121">Ele usa tipos no namespace <xref:System.IO.Packaging?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="e6eab-121">It uses types in the <xref:System.IO.Packaging?displayProperty=nameWithType> namespace.</span></span>

```csharp
const string documentRelationshipType =
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument";
const string wordmlNamespace =
  "http://schemas.openxmlformats.org/wordprocessingml/2006/main";
XNamespace w = wordmlNamespace;

using (Package wdPackage = Package.Open("SampleDoc.docx", FileMode.Open, FileAccess.Read))
{
    PackageRelationship relationship =
        wdPackage
        .GetRelationshipsByType(documentRelationshipType)
        .FirstOrDefault();
    if (relationship != null)
    {
        Uri documentUri =
            PackUriHelper.ResolvePartUri(
                new Uri("/", UriKind.Relative),
                relationship.TargetUri);
        PackagePart documentPart = wdPackage.GetPart(documentUri);

        //  Get the officeDocument part from the package.
        //  Load the XML in the part into an XDocument instance.
        XDocument xdoc =
            XDocument.Load(XmlReader.Create(documentPart.GetStream()));
        Console.WriteLine(xdoc.Root);
    }
}
```

```vb
Imports <xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main">

Module Module1
    Sub Main()
        Dim documentRelationshipType = _
          "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument"

        Using wdPackage As Package = _
          Package.Open("SampleDoc.docx", _
                       FileMode.Open, FileAccess.Read)
            Dim docPackageRelationship As PackageRelationship = wdPackage _
                .GetRelationshipsByType(documentRelationshipType).FirstOrDefault()
            If (docPackageRelationship IsNot Nothing) Then
                Dim documentUri As Uri = PackUriHelper.ResolvePartUri( _
                            New Uri("/", UriKind.Relative), _
                            docPackageRelationship.TargetUri)
                Dim documentPart As PackagePart = wdPackage.GetPart(documentUri)

                ' Get the officeDocument part from the package.
                ' Load the XML in the part into an XDocument instance.
                Dim xDoc As XDocument = _
                    XDocument.Load(XmlReader.Create(documentPart.GetStream()))
                Console.WriteLine(xDoc.Root)
            End If
        End Using
    End Sub
End Module
```

## <a name="see-also"></a><span data-ttu-id="e6eab-122">Confira também</span><span class="sxs-lookup"><span data-stu-id="e6eab-122">See also</span></span>

- <span data-ttu-id="e6eab-123">[Apresentando os formatos de arquivo do Office (2007) Open XML](/previous-versions/office/developer/office-2007/aa338205(v=office.12))</span><span class="sxs-lookup"><span data-stu-id="e6eab-123">[Introducing the Office (2007) Open XML File Formats](/previous-versions/office/developer/office-2007/aa338205(v=office.12))</span></span>
- <span data-ttu-id="e6eab-124">[Visão geral de WordprocessingML](/previous-versions/office/developer/office-2003/aa212812(v=office.11))</span><span class="sxs-lookup"><span data-stu-id="e6eab-124">[Overview of WordprocessingML](/previous-versions/office/developer/office-2003/aa212812(v=office.11))</span></span>
- [<span data-ttu-id="e6eab-125">Anatomia de um arquivo de WordProcessingML</span><span class="sxs-lookup"><span data-stu-id="e6eab-125">Anatomy of a WordProcessingML File</span></span>](http://officeopenxml.com/anatomyofOOXML.php)
- [<span data-ttu-id="e6eab-126">Introdução a WordprocessingML</span><span class="sxs-lookup"><span data-stu-id="e6eab-126">Introduction to WordprocessingML</span></span>](https://ericwhite.com/blog/introduction-to-wordprocessingml-series/)