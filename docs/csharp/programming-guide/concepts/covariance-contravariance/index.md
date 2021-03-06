---
title: Covariância e contravariância (C#)
description: Saiba mais sobre covariância e contravariância e como eles afetam a compatibilidade de atribuição. Consulte um exemplo de código que demonstra as diferenças entre eles.
ms.date: 07/20/2015
ms.assetid: 066d9a3c-aab7-4ea6-826d-0b1a85399c74
ms.openlocfilehash: ad4b2a7d7925d7893eb5a8e1d2d7c9ee3dcbd527
ms.sourcegitcommit: e7acba36517134238065e4d50bb4a1cfe47ebd06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2020
ms.locfileid: "89465657"
---
# <a name="covariance-and-contravariance-c"></a>Covariância e contravariância (C#)
No C#, a covariância e a contravariância habilitam a conversão de referência implícita para tipos de matriz, tipos de delegados e argumentos de tipo genérico. A covariância preserva a compatibilidade de atribuição, e a contravariância reverte.  
  
 O código a seguir demonstra a diferença entre a compatibilidade da atribuição, a covariância e a contravariância.  
  
```csharp  
// Assignment compatibility.
string str = "test";  
// An object of a more derived type is assigned to an object of a less derived type.
object obj = str;  
  
// Covariance.
IEnumerable<string> strings = new List<string>();  
// An object that is instantiated with a more derived type argument
// is assigned to an object instantiated with a less derived type argument.
// Assignment compatibility is preserved.
IEnumerable<object> objects = strings;  
  
// Contravariance.
// Assume that the following method is in the class:
// static void SetObject(object o) { }
Action<object> actObject = SetObject;  
// An object that is instantiated with a less derived type argument
// is assigned to an object instantiated with a more derived type argument.
// Assignment compatibility is reversed.
Action<string> actString = actObject;  
```  
  
 A covariância para matrizes permite a conversão implícita de uma matriz de um tipo mais derivado para uma matriz de um tipo menos derivado. Mas essa operação não é fortemente tipada, conforme mostrado no exemplo de código a seguir.  
  
```csharp  
object[] array = new String[10];  
// The following statement produces a run-time exception.  
// array[0] = 10;  
```  
  
 O suporte de covariância e contravariância aos grupos de método permite a correspondência de assinaturas de método com tipos de delegados. Isso permite atribuir a delegados não apenas os métodos que têm correspondência de assinaturas, mas também métodos que retornam tipos mais derivados (covariância) ou que aceitam parâmetros que têm tipos menos derivados (contravariância) do que o especificado pelo tipo delegado. Para obter mais informações, consulte [Variância em delegados (C#)](./variance-in-delegates.md) e [Usando variância em delegados (C#)](./using-variance-in-delegates.md).  
  
 O exemplo de código a seguir mostra o suporte da covariância e da contravariância para grupos de método.  
  
```csharp  
static object GetObject() { return null; }  
static void SetObject(object obj) { }  
  
static string GetString() { return ""; }  
static void SetString(string str) { }  
  
static void Test()  
{  
    // Covariance. A delegate specifies a return type as object,  
    // but you can assign a method that returns a string.  
    Func<object> del = GetString;  
  
    // Contravariance. A delegate specifies a parameter type as string,  
    // but you can assign a method that takes an object.  
    Action<string> del2 = SetObject;  
}  
```  
  
 No .NET Framework 4 e versões posteriores, o C# dá suporte à covariância e contravariância em interfaces e delegados genéricos e permite a conversão implícita de parâmetros de tipo genérico. Para obter mais informações, consulte [Variação em interfaces genéricas (C#)](./variance-in-generic-interfaces.md) e [Variação em delegados (C#)](./variance-in-delegates.md).  
  
 O exemplo de código a seguir mostra a conversão de referência implícita para interfaces genéricas.  
  
```csharp  
IEnumerable<String> strings = new List<String>();  
IEnumerable<Object> objects = strings;  
```  
  
 Uma interface ou delegado genérico será chamado *variante* se seus parâmetros genéricos forem declarados covariantes ou contravariantes. O C# permite que você crie suas próprias interfaces variantes e delegados. Para obter mais informações, consulte [Criando interfaces genéricas variantes (C#)](./creating-variant-generic-interfaces.md) e [Variação em delegados (C#)](./variance-in-delegates.md).  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Variância em interfaces genéricas (C#)](./variance-in-generic-interfaces.md)|Discute covariância e contravariância em interfaces genéricas e fornece uma lista de interfaces genéricas variadas no .NET.|  
|[Criando interfaces genéricas variáveis (C#)](./creating-variant-generic-interfaces.md)|Mostra como criar interfaces variantes personalizadas.|  
|[Usando variação em interfaces para Coleções Genéricas (C#)](./using-variance-in-interfaces-for-generic-collections.md)|Mostra como o suporte de covariância e contravariância nas interfaces <xref:System.Collections.Generic.IEnumerable%601> e <xref:System.IComparable%601> pode ajudar na reutilização do código.|  
|[Variação em delegados (C#)](./variance-in-delegates.md)|Discute covariância e contravariância em delegados genéricos e não genéricos e fornece uma lista de delegados genéricos de variantes no .NET.|  
|[Usando variação em delegados (C#)](./using-variance-in-delegates.md)|Mostra como usar o suporte de covariância e contravariância em delegados não genéricos para corresponder às assinaturas de método com tipos delegados.|  
|[Usando variação para delegados genéricos Func e Action (C#)](./using-variance-for-func-and-action-generic-delegates.md)|Mostra como o suporte de covariância e contravariância nos delegados `Func` e `Action` pode ajudar na reutilização do código.|
