---
title: Arquitetando aplicativos .NET nativos de nuvem para o Azure
description: Um guia para a criação de aplicativos nativos de nuvem que aproveitam contêineres, microservices e recursos sem servidor do Azure.
author: ardalis
ms.date: 03/07/2019
ms.openlocfilehash: ce9898366d0327dd619b36cdf1487229d9cda7f5
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71183038"
---
# <a name="architecting-cloud-native-net-applications-for-azure"></a><span data-ttu-id="2ccce-103">Arquitetando aplicativos .NET nativos de nuvem para o Azure</span><span class="sxs-lookup"><span data-stu-id="2ccce-103">Architecting Cloud Native .NET Applications for Azure</span></span>

![imagem da capa](./media/cover.png)

<span data-ttu-id="2ccce-105">PUBLICADO POR</span><span class="sxs-lookup"><span data-stu-id="2ccce-105">PUBLISHED BY</span></span>

<span data-ttu-id="2ccce-106">Divisão de Desenvolvedores Microsoft, equipes dos produtos .NET e Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2ccce-106">Microsoft Developer Division, .NET, and Visual Studio product teams</span></span>

<span data-ttu-id="2ccce-107">Uma divisão da Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="2ccce-107">A division of Microsoft Corporation</span></span>

<span data-ttu-id="2ccce-108">One Microsoft Way</span><span class="sxs-lookup"><span data-stu-id="2ccce-108">One Microsoft Way</span></span>

<span data-ttu-id="2ccce-109">Redmond, Washington 98052-6399</span><span class="sxs-lookup"><span data-stu-id="2ccce-109">Redmond, Washington 98052-6399</span></span>

<span data-ttu-id="2ccce-110">Copyright © 2019, Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="2ccce-110">Copyright © 2019 by Microsoft Corporation</span></span>

<span data-ttu-id="2ccce-111">Todos os direitos reservados.</span><span class="sxs-lookup"><span data-stu-id="2ccce-111">All rights reserved.</span></span> <span data-ttu-id="2ccce-112">Nenhuma parte do conteúdo deste guia pode ser reproduzida ou transmitida de nenhuma forma nem por nenhum meio sem a permissão por escrito do publicador.</span><span class="sxs-lookup"><span data-stu-id="2ccce-112">No part of the contents of this book may be reproduced or transmitted in any form or by any means without the written permission of the publisher.</span></span>

<span data-ttu-id="2ccce-113">Este manual é fornecido "no estado em que se encontra" e expressa os pontos de vista e as opiniões do autor.</span><span class="sxs-lookup"><span data-stu-id="2ccce-113">This book is provided “as-is” and expresses the author’s views and opinions.</span></span> <span data-ttu-id="2ccce-114">Os pontos de vista, as opiniões e as informações expressos neste livro, incluindo URLs e outras referências a sites da Internet, podem ser alteradas sem aviso prévio.</span><span class="sxs-lookup"><span data-stu-id="2ccce-114">The views, opinions, and information expressed in this book, including URL and other Internet website references, may change without notice.</span></span>

<span data-ttu-id="2ccce-115">Alguns exemplos aqui representados são fornecidos apenas para ilustração e são fictícios.</span><span class="sxs-lookup"><span data-stu-id="2ccce-115">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="2ccce-116">Nenhuma associação ou conexão real é intencional ou deve ser deduzida.</span><span class="sxs-lookup"><span data-stu-id="2ccce-116">No real association or connection is intended or should be inferred.</span></span>

<span data-ttu-id="2ccce-117">A Microsoft e as marcas comerciais listadas em https://www.microsoft.com na página da Web “Marcas comerciais” são marcas comerciais do grupo de empresas da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2ccce-117">Microsoft and the trademarks listed at https://www.microsoft.com on the “Trademarks” webpage are trademarks of the Microsoft group of companies.</span></span>

<span data-ttu-id="2ccce-118">Mac e macOS são marcas comerciais da Apple Inc.</span><span class="sxs-lookup"><span data-stu-id="2ccce-118">Mac and macOS are trademarks of Apple Inc.</span></span>

<span data-ttu-id="2ccce-119">O logotipo de baleia do Docker é uma marca registrada da Docker, Inc. usado mediante permissão.</span><span class="sxs-lookup"><span data-stu-id="2ccce-119">The Docker whale logo is a registered trademark of Docker, Inc. Used by permission.</span></span>

<span data-ttu-id="2ccce-120">Todas as outras marcas e logotipos são propriedade de seus respectivos proprietários.</span><span class="sxs-lookup"><span data-stu-id="2ccce-120">All other marks and logos are property of their respective owners.</span></span>

<span data-ttu-id="2ccce-121">Autor:</span><span class="sxs-lookup"><span data-stu-id="2ccce-121">Author:</span></span>

> <span data-ttu-id="2ccce-122">**Steve "ardalis" Smith** – Arquiteto de software e instrutor – [Ardalis.com](https://ardalis.com)</span><span class="sxs-lookup"><span data-stu-id="2ccce-122">**Steve "ardalis" Smith** - Software Architect and Trainer - [Ardalis.com](https://ardalis.com)</span></span>
>
> <span data-ttu-id="2ccce-123">**Rob Vettor** -Microsoft-principal arquiteto de sistema de nuvem/arquiteto de IP- [RobVettor.com](https://robvettor.com)</span><span class="sxs-lookup"><span data-stu-id="2ccce-123">**Rob Vettor** - Microsoft - Principal Cloud System Architect/IP Architect - [RobVettor.com](https://robvettor.com)</span></span>

<span data-ttu-id="2ccce-124">Participantes e revisores:</span><span class="sxs-lookup"><span data-stu-id="2ccce-124">Participants and Reviewers:</span></span>

> <span data-ttu-id="2ccce-125">**Cesar de la Torre**, gerente de programa principal, equipe do .net, Microsoft</span><span class="sxs-lookup"><span data-stu-id="2ccce-125">**Cesar De la Torre**, Principal Program Manager, .NET team, Microsoft</span></span>
>
> <span data-ttu-id="2ccce-126">**Nish Anil**, Gerente de Programa Sênior, Equipe .NET, Microsoft</span><span class="sxs-lookup"><span data-stu-id="2ccce-126">**Nish Anil**, Sr. Program Manager, .NET team, Microsoft</span></span>

<span data-ttu-id="2ccce-127">Editores:</span><span class="sxs-lookup"><span data-stu-id="2ccce-127">Editors:</span></span>

> <span data-ttu-id="2ccce-128">**Maira Wenzel**, Sr. Content Developer, .net Team, Microsoft</span><span class="sxs-lookup"><span data-stu-id="2ccce-128">**Maira Wenzel**, Sr. Content Developer, .NET team, Microsoft</span></span>

## <a name="who-should-use-this-guide"></a><span data-ttu-id="2ccce-129">Quem deve usar este guia</span><span class="sxs-lookup"><span data-stu-id="2ccce-129">Who should use this guide</span></span>

<span data-ttu-id="2ccce-130">O público-alvo deste guia é, principalmente, desenvolvedores, líderes de desenvolvimento e arquitetos interessados em aprender a criar aplicativos projetados para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="2ccce-130">The audience for this guide is mainly developers, development leads, and architects who are interested in learning how to build applications designed for the cloud.</span></span>

<span data-ttu-id="2ccce-131">Um público-alvo secundário são responsáveis pelas decisões técnicas que planejam escolher se desejam criar seus aplicativos usando uma abordagem nativa de nuvem.</span><span class="sxs-lookup"><span data-stu-id="2ccce-131">A secondary audience is technical decision-makers who plan to choose whether to build their applications using a cloud-native approach.</span></span>

## <a name="how-you-can-use-this-guide"></a><span data-ttu-id="2ccce-132">Como você pode usar este guia</span><span class="sxs-lookup"><span data-stu-id="2ccce-132">How you can use this guide</span></span>

<span data-ttu-id="2ccce-133">Este guia começa definindo a nuvem nativa e introduzindo um aplicativo de referência criado usando princípios e tecnologias nativas de nuvem.</span><span class="sxs-lookup"><span data-stu-id="2ccce-133">This guide begins by defining cloud native and introducing a reference application built using cloud-native principles and technologies.</span></span> <span data-ttu-id="2ccce-134">Além desses dois primeiros capítulos, o restante do livro é dividido em capítulos específicos focados em tópicos comuns à maioria dos aplicativos nativos de nuvem.</span><span class="sxs-lookup"><span data-stu-id="2ccce-134">Beyond these first two chapters, the rest of the book is broken up into specific chapters focused on topics common to most cloud-native applications.</span></span> <span data-ttu-id="2ccce-135">Você pode ir para qualquer um desses capítulos para saber mais sobre abordagens nativas de nuvem para:</span><span class="sxs-lookup"><span data-stu-id="2ccce-135">You can jump to any of these chapters to learn about cloud-native approaches to:</span></span>

- <span data-ttu-id="2ccce-136">Dados e acesso a dados</span><span class="sxs-lookup"><span data-stu-id="2ccce-136">Data and data access</span></span>
- <span data-ttu-id="2ccce-137">Padrões de comunicação</span><span class="sxs-lookup"><span data-stu-id="2ccce-137">Communication patterns</span></span>
- <span data-ttu-id="2ccce-138">Dimensionamento e escalabilidade</span><span class="sxs-lookup"><span data-stu-id="2ccce-138">Scaling and scalability</span></span>
- <span data-ttu-id="2ccce-139">Resiliência do aplicativo</span><span class="sxs-lookup"><span data-stu-id="2ccce-139">Application resiliency</span></span>
- <span data-ttu-id="2ccce-140">Monitoramento e integridade</span><span class="sxs-lookup"><span data-stu-id="2ccce-140">Monitoring and health</span></span>
- <span data-ttu-id="2ccce-141">Identidade e segurança</span><span class="sxs-lookup"><span data-stu-id="2ccce-141">Identity and security</span></span>
- <span data-ttu-id="2ccce-142">DevOps</span><span class="sxs-lookup"><span data-stu-id="2ccce-142">DevOps</span></span>

<span data-ttu-id="2ccce-143">Este guia está disponível em formato PDF e online.</span><span class="sxs-lookup"><span data-stu-id="2ccce-143">This guide is available both in PDF form and online.</span></span> <span data-ttu-id="2ccce-144">Fique à vontade para encaminhar este documento ou links para sua versão online para sua equipe para ajudar a garantir uma compreensão comum desses tópicos.</span><span class="sxs-lookup"><span data-stu-id="2ccce-144">Feel free to forward this document or links to its online version to your team to help ensure common understanding of these topics.</span></span> <span data-ttu-id="2ccce-145">A maioria desses tópicos se beneficia de uma compreensão consistente dos princípios e padrões subjacentes, bem como das compensações envolvidas em decisões relacionadas a esses tópicos.</span><span class="sxs-lookup"><span data-stu-id="2ccce-145">Most of these topics benefit from a consistent understanding of the underlying principles and patterns, as well as the trade-offs involved in decisions related to these topics.</span></span> <span data-ttu-id="2ccce-146">Nosso objetivo com este documento é equipar equipes e seus líderes com as informações de que precisam para tomar decisões bem informadas sobre a arquitetura, o desenvolvimento e a hospedagem dos seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2ccce-146">Our goal with this document is to equip teams and their leaders with the information they need to make well-informed decisions for their applications' architecture, development, and hosting.</span></span>

>[!div class="step-by-step"]
>[<span data-ttu-id="2ccce-147">Avançar</span><span class="sxs-lookup"><span data-stu-id="2ccce-147">Next</span></span>](introduction.md)