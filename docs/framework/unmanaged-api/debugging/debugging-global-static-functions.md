---
title: Depurando funções estáticas globais
ms.date: 03/30/2017
helpviewer_keywords:
- global static functions [.NET Framework debugging]
- debugging global static functions [.NET Framework]
- unmanaged global static functions [.NET Framework], debugging
ms.assetid: efc64414-77c3-48d0-881a-8594ed416aad
ms.openlocfilehash: c20d8719b63cb40074dc740506ae4a3c0fc3a251
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/28/2020
ms.locfileid: "76793776"
---
# <a name="debugging-global-static-functions"></a>Depurando funções estáticas globais
Esta seção descreve as funções estáticas globais não gerenciadas que a API de depuração usa.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Função _EFN_GetManagedExcepStack](efn-getmanagedexcepstack-function.md)  
 Dado um endereço de objeto de exceção gerenciado, retorna uma versão de cadeia de caracteres do rastreamento de pilha contido dentro.  
  
 [Função _EFN_GetManagedObjectFieldInfo](efn-getmanagedobjectfieldinfo-function.md)  
 Obtém o deslocamento do início de um objeto para um campo e o valor do campo, usando o ponteiro do objeto fornecido e o nome do campo.  
  
 [Função _EFN_GetManagedObjectName](efn-getmanagedobjectname-function.md)  
 Obtém o nome de um tipo usando o ponteiro de objeto gerenciado fornecido.  
  
 [Função _EFN_StackTrace](efn-stacktrace-function.md)  
 Fornece uma representação de texto de um rastreamento de pilha gerenciado e uma matriz de registros de `CONTEXT`, um para cada transição entre código gerenciado e não gerenciado.  
  
 [Função CLRDataCreateInstance](clrdatacreateinstance-function.md)  
 Chamado pelos serviços de acesso a dados do Common Language Runtime (CLR) para criar o objeto de interface especificado para o processo de destino especificado.  
  
 [Ponteiro de função PFN_CLRDataCreateInstance](pfn-clrdatacreateinstance-function-pointer.md)  
 Aponta para uma função que é chamada pelos serviços de acesso a dados do CLR para criar o objeto de interface especificado para o processo de destino especificado.  
  
## <a name="related-sections"></a>Seções Relacionadas  
 [Depurando coclasses](debugging-coclasses.md)  
  
 [Depurando interfaces](debugging-interfaces.md)  
  
 [Declarando enumerações](debugging-enumerations.md)  
  
 [Estruturas de depuração](debugging-structures.md)
