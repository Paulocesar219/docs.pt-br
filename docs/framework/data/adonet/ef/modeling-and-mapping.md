---
title: Modelando e mapeando
ms.date: 03/30/2017
ms.assetid: ec8a9515-3708-4cde-a688-4d8e6975f150
ms.openlocfilehash: 1488b2f6bd9dde5538144f886f1fb5e01ac0de3f
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90554925"
---
# <a name="modeling-and-mapping"></a>Modelando e mapeando
No Entity Framework, você pode definir o modelo conceitual, o modelo de armazenamento e o mapeamento entre os dois da maneira mais adequada para seu aplicativo. As ferramentas de Modelo de Dados de Entidade no Visual Studio permitem que você crie um. [arquivo EDMX](/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100)) de um banco de dados ou modelo gráfico e, em seguida, atualiza esse arquivo quando o banco de dados ou o modelo é alterado.  
  
 A partir do Entity Framework 4.1, você também pode criar um modelo programaticamente usando o desenvolvimento Code First. Há dois cenários diferentes para desenvolvimento Code First. Em ambos os casos, o desenvolvedor define um modelo codificando definições de classe do .NET Framework e, em seguida, opcionalmente especifica o mapeamento adicional ou a configuração usando Anotações de Dados ou a API fluente.  
  
 Para obter mais informações, consulte [criando um modelo](/ef/ef6/modeling/).  
  
 Você também pode usar o gerador EDM, que está incluído com o .NET Framework. O EdmGen.exe gera os arquivos .csdl, .ssdl e .msl de uma fonte de dados existente. Você também pode criar manualmente o modelo e o conteúdo do mapeamento. Para obter mais informações, consulte [EDM Generator (EdmGen.exe)](edm-generator-edmgen-exe.md).
