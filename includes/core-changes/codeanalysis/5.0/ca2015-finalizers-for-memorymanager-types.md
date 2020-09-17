---
ms.openlocfilehash: 4fc31f75e8f8cdd50abebd399d9749688e6faa5a
ms.sourcegitcommit: a69d548f90a03e105ee6701236c38390ecd9ccd1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/14/2020
ms.locfileid: "90065118"
---
### <a name="ca2015-do-not-define-finalizers-for-types-derived-from-memorymanagert"></a><span data-ttu-id="5cfde-101">CA2015: Não definir finalizadores para tipos derivados do MemoryManager\<T></span><span class="sxs-lookup"><span data-stu-id="5cfde-101">CA2015: Do not define finalizers for types derived from MemoryManager\<T></span></span>

<span data-ttu-id="5cfde-102">A regra do analisador de código .NET [CA2015](/visualstudio/code-quality/ca2015) está habilitada, por padrão, a partir do .NET 5,0.</span><span class="sxs-lookup"><span data-stu-id="5cfde-102">.NET code analyzer rule [CA2015](/visualstudio/code-quality/ca2015) is enabled, by default, starting in .NET 5.0.</span></span> <span data-ttu-id="5cfde-103">Ele produz um aviso de compilação para todos os tipos que derivam de <xref:System.Buffers.MemoryManager%601> que definem um finalizador.</span><span class="sxs-lookup"><span data-stu-id="5cfde-103">It produces a build warning for any types that derive from <xref:System.Buffers.MemoryManager%601> that define a finalizer.</span></span>

#### <a name="change-description"></a><span data-ttu-id="5cfde-104">Descrição das alterações</span><span class="sxs-lookup"><span data-stu-id="5cfde-104">Change description</span></span>

<span data-ttu-id="5cfde-105">A partir do .NET 5,0, o SDK do .NET inclui [analisadores de código-fonte .net](../../../../docs/fundamentals/productivity/code-analysis.md).</span><span class="sxs-lookup"><span data-stu-id="5cfde-105">Starting in .NET 5.0, the .NET SDK includes [.NET source code analyzers](../../../../docs/fundamentals/productivity/code-analysis.md).</span></span> <span data-ttu-id="5cfde-106">Várias dessas regras estão habilitadas, por padrão, incluindo [CA2015](/visualstudio/code-quality/ca2015).</span><span class="sxs-lookup"><span data-stu-id="5cfde-106">Several of these rules are enabled, by default, including [CA2015](/visualstudio/code-quality/ca2015).</span></span> <span data-ttu-id="5cfde-107">Se o seu projeto contiver código que viole essa regra e estiver configurado para tratar avisos como erros, essa alteração poderá interromper sua compilação.</span><span class="sxs-lookup"><span data-stu-id="5cfde-107">If your project contains code that violates this rule and is configured to treat warnings as errors, this change could break your build.</span></span>

<span data-ttu-id="5cfde-108">Os tipos de sinalizadores CA2015 de regra que derivam de <xref:System.Buffers.MemoryManager%601> que definem um finalizador.</span><span class="sxs-lookup"><span data-stu-id="5cfde-108">Rule CA2015 flags types that derive from <xref:System.Buffers.MemoryManager%601> that define a finalizer.</span></span> <span data-ttu-id="5cfde-109">A adição de um finalizador a um tipo derivado de <xref:System.Buffers.MemoryManager%601> é provavelmente uma indicação de um bug.</span><span class="sxs-lookup"><span data-stu-id="5cfde-109">Adding a finalizer to a type that derives from <xref:System.Buffers.MemoryManager%601> is likely an indication of a bug.</span></span> <span data-ttu-id="5cfde-110">Ele sugere que um recurso nativo que poderia ter sido obtido em um <xref:System.Span%601> está sendo limpo, possivelmente enquanto ainda está em uso pelo <xref:System.Span%601> .</span><span class="sxs-lookup"><span data-stu-id="5cfde-110">It suggests that a native resource that could have been obtained in a <xref:System.Span%601> is getting cleaned up, potentially while it's still in use by the <xref:System.Span%601>.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="5cfde-111">Versão introduzida</span><span class="sxs-lookup"><span data-stu-id="5cfde-111">Version introduced</span></span>

<span data-ttu-id="5cfde-112">5,0 Preview 8</span><span class="sxs-lookup"><span data-stu-id="5cfde-112">5.0 Preview 8</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="5cfde-113">Ação recomendada</span><span class="sxs-lookup"><span data-stu-id="5cfde-113">Recommended action</span></span>

- <span data-ttu-id="5cfde-114">Remova a definição do finalizador.</span><span class="sxs-lookup"><span data-stu-id="5cfde-114">Remove the finalizer definition.</span></span> <span data-ttu-id="5cfde-115">Para obter mais informações, consulte [CA2015](/visualstudio/code-quality/ca2015).</span><span class="sxs-lookup"><span data-stu-id="5cfde-115">For more information, see [CA2015](/visualstudio/code-quality/ca2015).</span></span>

- <span data-ttu-id="5cfde-116">Para desabilitar completamente a análise de código, defina `EnableNETAnalyzers` como `false` em seu arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="5cfde-116">To disable code analysis completely, set `EnableNETAnalyzers` to `false` in your project file.</span></span> <span data-ttu-id="5cfde-117">Para obter mais informações, consulte [EnableNETAnalyzers](../../../../docs/core/project-sdk/msbuild-props.md#enablenetanalyzers).</span><span class="sxs-lookup"><span data-stu-id="5cfde-117">For more information, see [EnableNETAnalyzers](../../../../docs/core/project-sdk/msbuild-props.md#enablenetanalyzers).</span></span>

#### <a name="category"></a><span data-ttu-id="5cfde-118">Categoria</span><span class="sxs-lookup"><span data-stu-id="5cfde-118">Category</span></span>

<span data-ttu-id="5cfde-119">Análise de código</span><span class="sxs-lookup"><span data-stu-id="5cfde-119">Code analysis</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="5cfde-120">APIs afetadas</span><span class="sxs-lookup"><span data-stu-id="5cfde-120">Affected APIs</span></span>

<span data-ttu-id="5cfde-121">Não detectável via análise de API.</span><span class="sxs-lookup"><span data-stu-id="5cfde-121">Not detectable via API analysis.</span></span>

<!--

#### Affected APIs

Not detectable via API analysis.

-->