---
title: Elemento <applicationPool> (configurações da Web)
ms.date: 03/30/2017
helpviewer_keywords:
- applicationPool element
- <applicationPool> element
ms.assetid: 46d1baaa-e343-4639-b70d-2a43a9f62b2a
ms.openlocfilehash: ca474cdcaeaac7b1c32efa5c58f4b5bb5b7f7895
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90557236"
---
# <a name="applicationpool-element-web-settings"></a>Elemento \<applicationPool> (configurações da Web)
Especifica as definições de configuração que são usadas pelo ASP.NET para gerenciar o comportamento de todo o processo quando um aplicativo ASP.NET está sendo executado no modo integrado no IIS 7,0 ou em uma versão posterior.  
  
> [!IMPORTANT]
> Esse elemento e o recurso que ele dá suporte só funcionarão se o aplicativo ASP.NET estiver hospedado no IIS 7,0 ou em versões posteriores.  
  
[**\<configuration>**](../configuration-element.md)  
&nbsp;&nbsp;[**\<system.web>**](system-web-element-web-settings.md)  
&nbsp;&nbsp;&nbsp;&nbsp;**\<applicationPool>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<applicationPool
    maxConcurrentRequestsPerCPU="5000"
    maxConcurrentThreadsPerCPU="0"
    requestQueueLimit="5000" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`maxConcurrentRequestsPerCPU`|Especifica quantas solicitações simultâneas o ASP.NET permite por CPU.|  
|`maxConcurrentThreadsPerCPU`|Especifica quantos threads simultâneos podem ser executados para um pool de aplicativos para cada CPU. Isso fornece uma maneira alternativa de controlar a simultaneidade ASP.NET, pois você pode limitar o número de threads gerenciados que podem ser usados por CPU para atender a solicitações. Por padrão, essa configuração é 0, o que significa que o ASP.NET não limita o número de threads que podem ser criados por CPU, embora o pool de threads do CLR também limite o número de threads que podem ser criados.|  
|`requestQueueLimit`|Especifica o número máximo de solicitações que podem ser enfileiradas para ASP.NET em um único processo. Quando dois ou mais aplicativos ASP.NET são executados em um único pool de aplicativos, o conjunto cumulativo de solicitações que estão sendo feitas a qualquer aplicativo no pool de aplicativos está sujeito a essa configuração.|  
  
### <a name="child-elements"></a>Elementos filho  
 Nenhum.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<system.web>](system-web-element-web-settings.md)|Contém informações sobre como o ASP.NET interage com um aplicativo host.|  
  
## <a name="remarks"></a>Comentários  

Quando você executa o IIS 7,0 ou uma versão posterior no modo integrado, essa combinação de elementos permite que você configure como o ASP.NET gerencia as solicitações de threads e filas quando o aplicativo é hospedado em um pool de aplicativos do IIS. Se você executar o IIS 6 ou executar o IIS 7,0 no modo clássico ou no modo ISAPI, essas configurações serão ignoradas.  
  
As `applicationPool` configurações se aplicam a todos os pools de aplicativos executados em uma versão específica do .NET Framework. As configurações estão contidas em um arquivo de aspnet.config. Há uma versão desse arquivo para as versões 2,0 e 4,0 do .NET Framework. (As versões 3,0 e 3,5 do .NET Framework compartilham o arquivo aspnet.config com a versão 2,0.)  
  
> [!IMPORTANT]
> Se você executar o IIS 7,0 no Windows 7, poderá configurar um arquivo de aspnet.config separado para cada pool de aplicativos. Isso permite que você personalize o desempenho dos threads para cada pool de aplicativos.  
  
Para a `maxConcurrentRequestsPerCPU` configuração, a configuração padrão de "5000" no .NET Framework 4 desativa efetivamente a limitação de solicitação controlada pelo ASP.net, a menos que você realmente tenha 5000 ou mais solicitações por CPU. A configuração padrão depende, em vez disso, do pool de threads CLR para gerenciar automaticamente a simultaneidade por CPU. Os aplicativos que fazem uso extensivo do processamento assíncrono de solicitações ou que têm muitas solicitações de execução longa bloqueadas na e/s de rede, se beneficiarão do maior limite padrão no .NET Framework 4. `maxConcurrentRequestsPerCPU`A configuração para zero desativa o uso de threads gerenciados para processar solicitações ASP.net. Quando um aplicativo é executado em um pool de aplicativos do IIS, as solicitações permanecem no thread de e/s do IIS e, portanto, a simultaneidade é limitada pelas configurações de thread do IIS.  
  
A `requestQueueLimit` configuração funciona da mesma maneira que o `requestQueueLimit` atributo do elemento [processModel](/previous-versions/dotnet/netframework-4.0/7w2sway1(v=vs.100)) , que é definido na Web.config arquivos para aplicativos ASP.net. No entanto, a `requestQueueLimit` configuração em um arquivo de aspnet.config substitui a `requestQueueLimit` configuração em um arquivo de Web.config. Em outras palavras, se ambos os atributos forem definidos (por padrão, isso é verdadeiro), a `requestQueueLimit` configuração no arquivo de aspnet.config terá precedência.  
  
## <a name="example"></a>Exemplo  

O exemplo a seguir mostra como configurar o comportamento de todo o processo do ASP.NET no arquivo de aspnet.config nas seguintes circunstâncias:  
  
- O aplicativo é hospedado em um pool de aplicativos do IIS 7,0.  
  
- O IIS 7,0 está sendo executado no modo integrado.  
  
- O aplicativo está usando o .NET Framework 3,5 SP1 ou uma versão posterior.  
  
Os valores no exemplo são os valores padrão.  
  
```xml  
<configuration>  
  <system.web>  
    <applicationPool
        maxConcurrentRequestsPerCPU="5000"  
        maxConcurrentThreadsPerCPU="0"
        requestQueueLimit="5000" />  
  </system.web>  
</configuration>  
```  
  
## <a name="element-information"></a>Informações do elemento  
  
|||  
|-|-|  
|Namespace||  
|Nome do Esquema||  
|Arquivo de validação||  
|Pode estar vazio||  
  
## <a name="see-also"></a>Confira também

- [\<system.web> Elemento (configurações da Web)](system-web-element-web-settings.md)
