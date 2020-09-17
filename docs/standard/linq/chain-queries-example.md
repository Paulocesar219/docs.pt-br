---
title: Exemplo de consultas de encadeamento (C#)-LINQ to XML
description: Saiba o que acontece quando você encadea duas consultas que usam a execução adiada e a avaliação lenta.
ms.date: 07/20/2015
ms.assetid: abbca162-d95e-43af-b92c-e46e6aa2540e
ms.openlocfilehash: c0bbab9061b98eda15523f8a8e64e997bde8b307
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552017"
---
# <a name="chain-queries-example-c-linq-to-xml"></a><span data-ttu-id="c98a5-103">Exemplo de consultas de encadeamento (C#) (LINQ to XML)</span><span class="sxs-lookup"><span data-stu-id="c98a5-103">Chain queries example (C#) (LINQ to XML)</span></span>

<span data-ttu-id="c98a5-104">Este exemplo baseia-se no exemplo no [exemplo de execução adiada](deferred-execution-example.md) e mostra o que acontece quando você encadea duas consultas que usam a execução adiada e a avaliação lenta.</span><span class="sxs-lookup"><span data-stu-id="c98a5-104">This example builds on the example in [Deferred execution example](deferred-execution-example.md) and shows what happens when you chain together two queries that both use deferred execution and lazy evaluation.</span></span>

## <a name="example-add-a-second-extension-method-that-uses-yield-return-to-defer-execution"></a><span data-ttu-id="c98a5-105">Exemplo: adicionar um segundo método de extensão que o usa `yield return` para adiar a execução</span><span class="sxs-lookup"><span data-stu-id="c98a5-105">Example: Add a second extension method that uses `yield return` to defer execution</span></span>

<span data-ttu-id="c98a5-106">Neste exemplo, outro método de extensão é introduzido, `AppendString` , que acrescenta uma cadeia de caracteres especificada em cada cadeia de caracteres na coleção de origem e, em seguida, produz a cadeia de caracteres alterada.</span><span class="sxs-lookup"><span data-stu-id="c98a5-106">In this example, another extension method is introduced, `AppendString`, which appends a specified string onto every string in the source collection, and then yields the changed string.</span></span>

```csharp
public static class LocalExtensions
{
    public static IEnumerable<string>
      ConvertCollectionToUpperCase(this IEnumerable<string> source)
    {
        foreach (string str in source)
        {
            Console.WriteLine("ToUpper: source >{0}<", str);
            yield return str.ToUpper();
        }
    }

    public static IEnumerable<string>
      AppendString(this IEnumerable<string> source, string stringToAppend)
    {
        foreach (string str in source)
        {
            Console.WriteLine("AppendString: source >{0}<", str);
            yield return str + stringToAppend;
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        string[] stringArray = { "abc", "def", "ghi" };

        IEnumerable<string> q1 =
            from s in stringArray.ConvertCollectionToUpperCase()
            select s;

        IEnumerable<string> q2 =
            from s in q1.AppendString("!!!")
            select s;

        foreach (string str in q2)
        {
            Console.WriteLine("Main: str >{0}<", str);
            Console.WriteLine();
        }
    }
}
```

 <span data-ttu-id="c98a5-107">Esse exemplo gera a saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="c98a5-107">This example produces the following output:</span></span>

```output
ToUpper: source >abc<
AppendString: source >ABC<
Main: str >ABC!!!<

ToUpper: source >def<
AppendString: source >DEF<
Main: str >DEF!!!<

ToUpper: source >ghi<
AppendString: source >GHI<
Main: str >GHI!!!<
```

<span data-ttu-id="c98a5-108">Nesse exemplo, você pode ver que cada método de extensão opera um de cada vez para cada item na coleção de origem.</span><span class="sxs-lookup"><span data-stu-id="c98a5-108">In this example, you can see that each extension method operates one at a time for each item in the source collection.</span></span>

<span data-ttu-id="c98a5-109">O que deve ser claro desse exemplo é o mesmo que nós encadeemos juntos consultas que rendem coleções, qualquer coleção intermediária é materializada.</span><span class="sxs-lookup"><span data-stu-id="c98a5-109">What should be clear from this example is that even though we have chained together queries that yield collections, no intermediate collections are materialized.</span></span> <span data-ttu-id="c98a5-110">Em vez disso, cada item é passado de um método lenta a seguir.</span><span class="sxs-lookup"><span data-stu-id="c98a5-110">Instead, each item is passed from one lazy method to the next.</span></span> <span data-ttu-id="c98a5-111">Isso resulta em uma pegada muito menor de memória do que uma abordagem que recebe primeiro uma matriz de cadeias de caracteres, então cria uma segunda matriz de cadeias de caracteres que foram convertidos para maiúsculas, e criar finalmente uma terceira matriz de cadeias de caracteres onde cada cadeia de caracteres tem os pontos de exclamação acrescentados a ele.</span><span class="sxs-lookup"><span data-stu-id="c98a5-111">This results in a much smaller memory footprint than an approach that would first take one array of strings, then create a second array of strings that have been converted to uppercase, and finally create a third array of strings where each string has the exclamation points appended to it.</span></span>

<span data-ttu-id="c98a5-112">O próximo artigo deste tutorial ilustra a materialização intermediária:</span><span class="sxs-lookup"><span data-stu-id="c98a5-112">The next article in this tutorial illustrates intermediate materialization:</span></span>

- [<span data-ttu-id="c98a5-113">Materialização intermediária (C#)</span><span class="sxs-lookup"><span data-stu-id="c98a5-113">Intermediate materialization (C#)</span></span>](intermediate-materialization.md)

## <a name="see-also"></a><span data-ttu-id="c98a5-114">Confira também</span><span class="sxs-lookup"><span data-stu-id="c98a5-114">See also</span></span>

- [<span data-ttu-id="c98a5-115">Execução retardada e avaliação lenta</span><span class="sxs-lookup"><span data-stu-id="c98a5-115">Deferred execution and lazy evaluation</span></span>](deferred-execution-lazy-evaluation.md)