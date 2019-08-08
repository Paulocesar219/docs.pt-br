---
title: Testar aplicativos ASP.NET Core MVC
description: Projetar aplicativos Web modernos com o ASP.NET Core e o Azure | Testar aplicativos ASP.NET Core MVC
author: ardalis
ms.author: wiwagn
ms.date: 01/30/2019
ms.openlocfilehash: 941c73f9a8b7b4c4336adfaec45775feec738f51
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68672873"
---
# <a name="test-aspnet-core-mvc-apps"></a><span data-ttu-id="3b1cc-103">Testar aplicativos ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="3b1cc-103">Test ASP.NET Core MVC apps</span></span>

> <span data-ttu-id="3b1cc-104">*"Se você não gostar de realizar o teste de unidade em seu produto, provavelmente, seus clientes não vão gostar de testá-lo também."*</span><span class="sxs-lookup"><span data-stu-id="3b1cc-104">*"If you don't like unit testing your product, most likely your customers won't like to test it, either."*</span></span>
 > <span data-ttu-id="3b1cc-105">\_ – Anônimo –</span><span class="sxs-lookup"><span data-stu-id="3b1cc-105">\_- Anonymous-</span></span>

<span data-ttu-id="3b1cc-106">Um software de qualquer complexidade pode falhar de maneiras inesperadas em resposta a alterações.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-106">Software of any complexity can fail in unexpected ways in response to changes.</span></span> <span data-ttu-id="3b1cc-107">Portanto, depois de fazer alterações, é necessário realizar um teste em todos os aplicativos, exceto os mais triviais (ou menos críticos).</span><span class="sxs-lookup"><span data-stu-id="3b1cc-107">Thus, testing after making changes is required for all but the most trivial (or least critical) applications.</span></span> <span data-ttu-id="3b1cc-108">O teste manual é a maneira mais lenta, menos confiável e mais cara de testar um software.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-108">Manual testing is the slowest, least reliable, most expensive way to test software.</span></span> <span data-ttu-id="3b1cc-109">Se os aplicativos não forem projetados para serem testáveis, esse poderá ser o único meio disponível.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-109">Unfortunately, if applications aren't designed to be testable, it can be the only means available.</span></span> <span data-ttu-id="3b1cc-110">Os aplicativos escritos de acordo com os princípios de arquitetura apresentados no [capítulo 4](architectural-principles.md) podem ser submetidos a um teste de unidade, além disso os aplicativos ASP.NET Core também são compatíveis com testes funcionais e de integração automatizados.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-110">Applications written following the architectural principles laid out in [chapter 4](architectural-principles.md) should be unit testable, and ASP.NET Core applications support automated integration and functional testing as well.</span></span>

## <a name="kinds-of-automated-tests"></a><span data-ttu-id="3b1cc-111">Tipos de testes automatizados</span><span class="sxs-lookup"><span data-stu-id="3b1cc-111">Kinds of automated tests</span></span>

<span data-ttu-id="3b1cc-112">Há muitos tipos de testes automatizados para aplicativos de software.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-112">There are many kinds of automated tests for software applications.</span></span> <span data-ttu-id="3b1cc-113">O teste mais simples de nível mais baixo é o teste de unidade.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-113">The simplest, lowest level test is the unit test.</span></span> <span data-ttu-id="3b1cc-114">Em um nível ligeiramente superior, há testes de integração e testes funcionais.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-114">At a slightly higher level there are integration tests and functional tests.</span></span> <span data-ttu-id="3b1cc-115">Outros tipos de testes, como testes de interface do usuário, testes de carga, testes de estresse e smoke tests, estão além do escopo deste documento.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-115">Other kinds of tests, like UI tests, load tests, stress tests, and smoke tests, are beyond the scope of this document.</span></span>

### <a name="unit-tests"></a><span data-ttu-id="3b1cc-116">Testes de unidade</span><span class="sxs-lookup"><span data-stu-id="3b1cc-116">Unit tests</span></span>

<span data-ttu-id="3b1cc-117">Um teste de unidade testa uma única parte da lógica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-117">A unit test tests a single part of your application's logic.</span></span> <span data-ttu-id="3b1cc-118">Ainda podemos descrevê-lo listando algumas das coisas que ele não é.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-118">One can further describe it by listing some of the things that it isn't.</span></span> <span data-ttu-id="3b1cc-119">Um teste de unidade não testa como o código funciona com as dependências ou a infraestrutura – é para isso que servem os testes de integração.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-119">A unit test doesn't test how your code works with dependencies or infrastructure – that's what integration tests are for.</span></span> <span data-ttu-id="3b1cc-120">Um teste de unidade não testa a estrutura na qual o código foi escrito – você deve pressupor que ela funciona ou, se achar que não, registre um bug e codifique uma solução alternativa.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-120">A unit test doesn't test the framework your code is written on – you should assume it works or, if you find it doesn't, file a bug and code a workaround.</span></span> <span data-ttu-id="3b1cc-121">Um teste de unidade é executado completamente na memória e no processo.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-121">A unit test runs completely in memory and in process.</span></span> <span data-ttu-id="3b1cc-122">Ele não se comunica com o sistema de arquivos, a rede ou um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-122">It doesn't communicate with the file system, the network, or a database.</span></span> <span data-ttu-id="3b1cc-123">Os testes de unidade devem testar apenas o código.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-123">Unit tests should only test your code.</span></span>

<span data-ttu-id="3b1cc-124">Os testes de unidade, devido ao fato de testarem apenas uma única unidade do código, sem dependências externas, devem ser executados muito rapidamente.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-124">Unit tests, by virtue of the fact that they test only a single unit of your code, with no external dependencies, should execute extremely quickly.</span></span> <span data-ttu-id="3b1cc-125">Portanto, você deve conseguir executar conjuntos de testes de centenas de testes de unidade em alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-125">Thus, you should be able to run test suites of hundreds of unit tests in a few seconds.</span></span> <span data-ttu-id="3b1cc-126">Execute-os com frequência, de preferência, antes de cada push para um repositório de controle do código-fonte compartilhado e, certamente, a cada build automatizado no servidor de build.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-126">Run them frequently, ideally before every push to a shared source control repository, and certainly with every automated build on your build server.</span></span>

### <a name="integration-tests"></a><span data-ttu-id="3b1cc-127">Testes de integração</span><span class="sxs-lookup"><span data-stu-id="3b1cc-127">Integration tests</span></span>

<span data-ttu-id="3b1cc-128">Embora seja uma boa ideia encapsular o código que interage com a infraestrutura, como bancos de dados e sistemas de arquivos, você ainda terá uma parte do código e, provavelmente, desejará testá-lo.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-128">Although it's a good idea to encapsulate your code that interacts with infrastructure like databases and file systems, you will still have some of that code, and you will probably want to test it.</span></span> <span data-ttu-id="3b1cc-129">Além disso, você deve verificar se as camadas do código interagem conforme esperado quando as dependências do aplicativo são totalmente resolvidas.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-129">Additionally, you should verify that your code's layers interact as you expect when your application's dependencies are fully resolved.</span></span> <span data-ttu-id="3b1cc-130">Essa é a responsabilidade dos testes de integração.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-130">This is the responsibility of integration tests.</span></span> <span data-ttu-id="3b1cc-131">Os testes de integração tendem a ser mais lentos e mais difíceis de serem configurados do que os testes de unidade, porque geralmente dependem de infraestrutura e dependências externas.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-131">Integration tests tend to be slower and more difficult to set up than unit tests, because they often depend on external dependencies and infrastructure.</span></span> <span data-ttu-id="3b1cc-132">Portanto, você deve evitar testar coisas que podem ser testadas com testes de unidade em testes de integração.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-132">Thus, you should avoid testing things that could be tested with unit tests in integration tests.</span></span> <span data-ttu-id="3b1cc-133">Se puder testar determinado cenário com um teste de unidade, você deverá testá-lo com um teste de unidade.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-133">If you can test a given scenario with a unit test, you should test it with a unit test.</span></span> <span data-ttu-id="3b1cc-134">Caso contrário, considere o uso de um teste de integração.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-134">If you can't, then consider using an integration test.</span></span>

<span data-ttu-id="3b1cc-135">Os testes de integração costumam ter procedimentos de instalação e de desinstalação mais complexos em comparação com os testes de unidade.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-135">Integration tests will often have more complex setup and teardown procedures than unit tests.</span></span> <span data-ttu-id="3b1cc-136">Por exemplo, um teste de integração feito em um banco de dados real precisará de uma maneira de retornar o banco de dados para um estado conhecido antes de cada execução de teste.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-136">For example, an integration test that goes against an actual database will need a way to return the database to a known state before each test run.</span></span> <span data-ttu-id="3b1cc-137">Conforme novos testes forem adicionados e o esquema de banco de dados de produção evoluir, esses scripts de teste tenderão a aumentar em tamanho e complexidade.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-137">As new tests are added and the production database schema evolves, these test scripts will tend to grow in size and complexity.</span></span> <span data-ttu-id="3b1cc-138">Em muitos sistemas grandes, não é prático executar conjuntos completos de testes de integração em estações de trabalho do desenvolvedor antes de fazer check-in das alterações no controle do código-fonte compartilhado.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-138">In many large systems, it is impractical to run full suites of integration tests on developer workstations before checking in changes to shared source control.</span></span> <span data-ttu-id="3b1cc-139">Nesses casos, os testes de integração podem ser executados em um servidor de build.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-139">In these cases, integration tests may be run on a build server.</span></span>

<span data-ttu-id="3b1cc-140">A classe de implementação `LocalFileImageService` implementa a lógica para buscar e retornar os bytes de um arquivo de imagem de uma pasta específica, considerando uma ID:</span><span class="sxs-lookup"><span data-stu-id="3b1cc-140">The `LocalFileImageService` implementation class implements the logic for fetching and returning the bytes of an image file from a particular folder given an id:</span></span>

```csharp
public class LocalFileImageService : IImageService
{
    private readonly IHostingEnvironment _env;
    public LocalFileImageService(IHostingEnvironment env)
    {
        _env = env;
    }
    public byte[] GetImageBytesById(int id)
    {
        try
        {
            var contentRoot = _env.ContentRootPath + "//Pics";
            var path = Path.Combine(contentRoot, id + ".png");
            return File.ReadAllBytes(path);
        }
        catch (FileNotFoundException ex)
        {
            throw new CatalogImageMissingException(ex);
        }
    }
}
```

### <a name="functional-tests"></a><span data-ttu-id="3b1cc-141">Testes funcionais</span><span class="sxs-lookup"><span data-stu-id="3b1cc-141">Functional tests</span></span>

<span data-ttu-id="3b1cc-142">Os testes de integração são escritos da perspectiva do desenvolvedor, para verificar se alguns componentes do sistema funcionam corretamente juntos.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-142">Integration tests are written from the perspective of the developer, to verify that some components of the system work correctly together.</span></span> <span data-ttu-id="3b1cc-143">Os testes funcionais são escritos da perspectiva do usuário e verificam a correção do sistema com base em seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-143">Functional tests are written from the perspective of the user, and verify the correctness of the system based on its requirements.</span></span> <span data-ttu-id="3b1cc-144">O trecho a seguir oferece uma analogia útil de como considerar os testes funcionais, em comparação com os testes de unidade:</span><span class="sxs-lookup"><span data-stu-id="3b1cc-144">The following excerpt offers a useful analogy for how to think about functional tests, compared to unit tests:</span></span>

> <span data-ttu-id="3b1cc-145">"Muitas vezes, o desenvolvimento de um sistema é comparado à construção de uma casa.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-145">"Many times the development of a system is likened to the building of a house.</span></span> <span data-ttu-id="3b1cc-146">Embora essa analogia não seja muito correta, podemos estendê-la para compreender a diferença entre os testes de unidade e os testes funcionais.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-146">While this analogy isn't quite correct, we can extend it for the purposes of understanding the difference between unit and functional tests.</span></span> <span data-ttu-id="3b1cc-147">O teste de unidade se assemelha a um inspetor de construção visitando o canteiro de obras de uma casa.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-147">Unit testing is analogous to a building inspector visiting a house's construction site.</span></span> <span data-ttu-id="3b1cc-148">Ele está concentrado nos vários sistemas internos da casa, na base, na estrutura, na parte elétrica, no encanamento e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-148">He is focused on the various internal systems of the house, the foundation, framing, electrical, plumbing, and so on.</span></span> <span data-ttu-id="3b1cc-149">Ele garante (testa) que as partes da casa funcionarão corretamente e com segurança, ou seja, seguirão o código de construção.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-149">He ensures (tests) that the parts of the house will work correctly and safely, that is, meet the building code.</span></span> <span data-ttu-id="3b1cc-150">Os testes funcionais, neste cenário, se assemelham ao proprietário da casa visitando esse mesmo canteiro de obras.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-150">Functional tests in this scenario are analogous to the homeowner visiting this same construction site.</span></span> <span data-ttu-id="3b1cc-151">Ele pressupõe que os sistemas internos se comportarão corretamente e que o inspetor de construção está realizando sua tarefa.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-151">He assumes that the internal systems will behave appropriately, that the building inspector is performing his task.</span></span> <span data-ttu-id="3b1cc-152">O proprietário da casa está voltado para a ideia de como será morar nessa casa.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-152">The homeowner is focused on what it will be like to live in this house.</span></span> <span data-ttu-id="3b1cc-153">Ele está preocupado com a aparência da casa, se os vários quartos têm um tamanho confortável, se a casa atende às necessidades da família, se as janelas estão em um bom lugar para capturar o sol da manhã.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-153">He is concerned with how the house looks, are the various rooms a comfortable size, does the house fit the family's needs, are the windows in a good spot to catch the morning sun.</span></span> <span data-ttu-id="3b1cc-154">O proprietário da casa está realizando testes funcionais na casa.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-154">The homeowner is performing functional tests on the house.</span></span> <span data-ttu-id="3b1cc-155">Ele tem a perspectiva do usuário.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-155">He has the user's perspective.</span></span> <span data-ttu-id="3b1cc-156">O inspetor de construção está realizando testes de unidade na casa.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-156">The building inspector is performing unit tests on the house.</span></span> <span data-ttu-id="3b1cc-157">Ele tem a perspectiva do construtor."</span><span class="sxs-lookup"><span data-stu-id="3b1cc-157">He has the builder's perspective."</span></span>

<span data-ttu-id="3b1cc-158">Fonte: [Unit Testing versus Functional Tests (Teste de unidade versus testes funcionais)](https://www.softwaretestingtricks.com/2007/01/unit-testing-versus-functional-tests.html)</span><span class="sxs-lookup"><span data-stu-id="3b1cc-158">Source: [Unit Testing versus Functional Tests](https://www.softwaretestingtricks.com/2007/01/unit-testing-versus-functional-tests.html)</span></span>

<span data-ttu-id="3b1cc-159">Gosto de dizer que "como desenvolvedores, falhamos de duas maneiras: criamos a coisa da maneira errada ou criamos a coisa errada".</span><span class="sxs-lookup"><span data-stu-id="3b1cc-159">I'm fond of saying "As developers, we fail in two ways: we build the thing wrong, or we build the wrong thing."</span></span> <span data-ttu-id="3b1cc-160">Os testes de unidade garantem que você está criando a coisa da maneira certa; os testes funcionais garantem que você está criando a coisa certa.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-160">Unit tests ensure you are building the thing right; functional tests ensure you are building the right thing.</span></span>

<span data-ttu-id="3b1cc-161">Como os testes funcionais operam no nível do sistema, eles podem exigir um certo grau de automação da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-161">Since functional tests operate at the system level, they may require some degree of UI automation.</span></span> <span data-ttu-id="3b1cc-162">Assim como os testes de integração, elas geralmente funcionam com algum tipo de infraestrutura de teste também.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-162">Like integration tests, they usually work with some kind of test infrastructure as well.</span></span> <span data-ttu-id="3b1cc-163">Isso faz com que eles fiquem mais lentos e mais frágeis do que os testes de unidade e de integração.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-163">This makes them slower and more brittle than unit and integration tests.</span></span> <span data-ttu-id="3b1cc-164">Você deve ter somente a quantidade de testes funcionais de que precisa para ter certeza de que o sistema está se comportando conforme esperado pelos usuários.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-164">You should have only as many functional tests as you need to be confident the system is behaving as users expect.</span></span>

### <a name="testing-pyramid"></a><span data-ttu-id="3b1cc-165">Pirâmide de testes</span><span class="sxs-lookup"><span data-stu-id="3b1cc-165">Testing Pyramid</span></span>

<span data-ttu-id="3b1cc-166">Martin Fowler escreveu sobre a pirâmide de testes, cujo exemplo é mostrado na Figura 9-1.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-166">Martin Fowler wrote about the testing pyramid, an example of which is shown in Figure 9-1.</span></span>

![](./media/image9-1.png)

<span data-ttu-id="3b1cc-167">Figura 9-1 Pirâmide de testes</span><span class="sxs-lookup"><span data-stu-id="3b1cc-167">Figure 9-1 Testing Pyramid</span></span>

<span data-ttu-id="3b1cc-168">As diferentes camadas da pirâmide e seus tamanhos relativos representam tipos diferentes de testes e quantos você deve gravar para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-168">The different layers of the pyramid, and their relative sizes, represent different kinds of tests and how many you should write for your application.</span></span> <span data-ttu-id="3b1cc-169">Como você pode ver, a recomendação é ter uma grande base de testes de unidade, apoiada por uma camada menor de testes de integração, com uma camada ainda menor de testes funcionais.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-169">As you can see, the recommendation is to have a large base of unit tests, supported by a smaller layer of integration tests, with an even smaller layer of functional tests.</span></span> <span data-ttu-id="3b1cc-170">O ideal é que cada camada tenha somente testes que não podem ser realizados de forma adequada em uma camada inferior.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-170">Each layer should ideally only have tests in it that cannot be performed adequately at a lower layer.</span></span> <span data-ttu-id="3b1cc-171">Lembre-se da pirâmide de testes quando estiver tentando decidir qual tipo de teste é necessário para um cenário específico.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-171">Keep the testing pyramid in mind when you are trying to decide which kind of test you need for a particular scenario.</span></span>

### <a name="what-to-test"></a><span data-ttu-id="3b1cc-172">O que testar</span><span class="sxs-lookup"><span data-stu-id="3b1cc-172">What to test</span></span>

<span data-ttu-id="3b1cc-173">Um problema comum para os desenvolvedores que não têm experiência com a criação de testes automatizados é decidir o que testar.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-173">A common problem for developers who are inexperienced with writing automated tests is coming up with what to test.</span></span> <span data-ttu-id="3b1cc-174">Um bom ponto de partida é testar a lógica condicional do teste.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-174">A good starting point is to test conditional logic.</span></span> <span data-ttu-id="3b1cc-175">Sempre que você tiver um método com um comportamento que é alterado de acordo com uma instrução condicional (if-else, alternância, etc.), você deverá pensar em, pelo menos, dois testes que confirmem esse comportamento correto em determinadas condições.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-175">Anywhere you have a method with behavior that changes based on a conditional statement (if-else, switch, etc.), you should be able to come up at least a couple of tests that confirm the correct behavior for certain conditions.</span></span> <span data-ttu-id="3b1cc-176">Se o código apresentar condições de erro, será melhor gravar, pelo menos, um teste para o "caminho certo" pelo código (sem erros) e, pelo menos, um teste para o "caminho errado" (com erros ou resultados atípicos) para confirmar que o aplicativo se comporta conforme esperado em caso de erros.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-176">If your code has error conditions, it's good to write at least one test for the "happy path" through the code (with no errors), and at least one test for the "sad path" (with errors or atypical results) to confirm your application behaves as expected in the face of errors.</span></span> <span data-ttu-id="3b1cc-177">Por fim, tente se concentrar no teste de coisas que podem falhar, em vez de se concentrar em métricas como cobertura de código.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-177">Finally, try to focus on testing things that can fail, rather than focusing on metrics like code coverage.</span></span> <span data-ttu-id="3b1cc-178">Em geral, mais cobertura de código é melhor do que menos.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-178">More code coverage is better than less, generally.</span></span> <span data-ttu-id="3b1cc-179">No entanto, é melhor utilizar o tempo criando mais alguns testes de um método muito complexo e comercialmente crítico do que criando testes para propriedades automáticas, apenas para melhorar as métricas de cobertura de código de teste.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-179">However, writing a few more tests of a very complex and business-critical method is usually a better use of time than writing tests for auto-properties just to improve test code coverage metrics.</span></span>

## <a name="organizing-test-projects"></a><span data-ttu-id="3b1cc-180">Organizando projetos de teste</span><span class="sxs-lookup"><span data-stu-id="3b1cc-180">Organizing test projects</span></span>

<span data-ttu-id="3b1cc-181">Os projetos de teste podem ser organizados da maneira mais adequada à sua situação.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-181">Test projects can be organized however works best for you.</span></span> <span data-ttu-id="3b1cc-182">É uma boa ideia separar os testes por tipo (teste de unidade, teste de integração) e pelo que eles estão testando (por projeto, por namespace).</span><span class="sxs-lookup"><span data-stu-id="3b1cc-182">It's a good idea to separate tests by type (unit test, integration test) and by what they are testing (by project, by namespace).</span></span> <span data-ttu-id="3b1cc-183">Indicar se essa separação consiste em pastas dentro de um único projeto de teste ou de vários projetos de teste é uma decisão de design.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-183">Whether this separation consists of folders within a single test project, or multiple test projects, is a design decision.</span></span> <span data-ttu-id="3b1cc-184">Um projeto é o mais simples, mas para projetos grandes com muitos testes ou para executar diferentes conjuntos de testes com mais facilidade, talvez você deseje ter vários projetos de teste diferentes.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-184">One project is simplest, but for large projects with many tests, or in order to more easily run different sets of tests, you might want to have several different test projects.</span></span> <span data-ttu-id="3b1cc-185">Muitas equipes organizam projetos de teste com base no projeto que estão testando, o que, para aplicativos com mais de alguns projetos, pode resultar em um grande número de projetos de teste, especialmente se você ainda divide-os de acordo com o tipo de testes existente em cada projeto.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-185">Many teams organize test projects based on the project they are testing, which for applications with more than a few projects can result in a large number of test projects, especially if you still break these down according to what kind of tests are in each project.</span></span> <span data-ttu-id="3b1cc-186">Uma abordagem de meio-termo é ter um projeto por tipo de teste, por aplicativo, com pastas dentro dos projetos de teste para indicar o projeto (e a classe) que está sendo testado.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-186">A compromise approach is to have one project per kind of test, per application, with folders inside the test projects to indicate the project (and class) being tested.</span></span>

<span data-ttu-id="3b1cc-187">Uma abordagem comum é organizar os projetos de aplicativo em uma pasta 'src' e os projetos de teste do aplicativo em uma pasta 'tests' paralela.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-187">A common approach is to organize the application projects under a ‘src' folder, and the application's test projects under a parallel ‘tests' folder.</span></span> <span data-ttu-id="3b1cc-188">Crie pastas de solução correspondentes no Visual Studio se achar esta organização útil.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-188">You can create matching solution folders in Visual Studio, if you find this organization useful.</span></span>

![](./media/image9-2.png)

<span data-ttu-id="3b1cc-189">Figura 9-2 Organização de testes na solução</span><span class="sxs-lookup"><span data-stu-id="3b1cc-189">Figure 9-2 Test organization in your solution</span></span>

<span data-ttu-id="3b1cc-190">Você pode usar qualquer estrutura de teste que preferir.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-190">You can use whichever test framework you prefer.</span></span> <span data-ttu-id="3b1cc-191">A estrutura xUnit funciona bem e é nela em que todos os testes do ASP.NET Core e do EF Core são criados.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-191">The xUnit framework works well and is what all of the ASP.NET Core and EF Core tests are written in.</span></span> <span data-ttu-id="3b1cc-192">Você pode adicionar um projeto de teste do xUnit no Visual Studio usando o modelo mostrado na Figura 9-3 ou por meio da CLI usando o comando dotnet new xunit.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-192">You can add an xUnit test project in Visual Studio using the template shown in Figure 9-3, or from the CLI using dotnet new xunit.</span></span>

![](./media/image9-3.png)

<span data-ttu-id="3b1cc-193">Figura 9-3 Adicionar um projeto de teste do xUnit no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3b1cc-193">Figure 9-3 Add an xUnit Test Project in Visual Studio</span></span>

### <a name="test-naming"></a><span data-ttu-id="3b1cc-194">Nomenclatura de testes</span><span class="sxs-lookup"><span data-stu-id="3b1cc-194">Test naming</span></span>

<span data-ttu-id="3b1cc-195">Você deve nomear os testes de maneira consistente, com nomes que indicam o que cada teste faz.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-195">You should name your tests in a consistent fashion, with names that indicate what each test does.</span></span> <span data-ttu-id="3b1cc-196">Uma abordagem na qual tive grande sucesso é nomear as classes de teste de acordo com a classe e o método que elas estão testando.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-196">One approach I've had great success with is to name test classes according to the class and method they are testing.</span></span> <span data-ttu-id="3b1cc-197">Isso resulta em muitas classes de teste pequenas, mas deixa extremamente claro pelo que é responsável cada teste.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-197">This results in many small test classes, but it makes it extremely clear what each test is responsible for.</span></span> <span data-ttu-id="3b1cc-198">Com o nome da classe de teste configurado para identificar a classe e o método a serem testados, o nome do método de teste pode ser usado para especificar o comportamento que está sendo testado.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-198">With the test class name set up to identify the class and method to be tested, the test method name can be used to specify the behavior being tested.</span></span> <span data-ttu-id="3b1cc-199">Isso deve incluir o comportamento esperado e as entradas ou suposições que devem gerar esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-199">This should include the expected behavior and any inputs or assumptions that should yield this behavior.</span></span> <span data-ttu-id="3b1cc-200">Alguns nomes de teste de exemplo:</span><span class="sxs-lookup"><span data-stu-id="3b1cc-200">Some example test names:</span></span>

- `CatalogControllerGetImage.CallsImageServiceWithId`

- `CatalogControllerGetImage.LogsWarningGivenImageMissingException`

- `CatalogControllerGetImage.ReturnsFileResultWithBytesGivenSuccess`

- `CatalogControllerGetImage.ReturnsNotFoundResultGivenImageMissingException`

<span data-ttu-id="3b1cc-201">Uma variação dessa abordagem termina o nome de cada classe de teste com "Should" e modifica ligeiramente os tempos verbais:</span><span class="sxs-lookup"><span data-stu-id="3b1cc-201">A variation of this approach ends each test class name with "Should" and modifies the tense slightly:</span></span>

- <span data-ttu-id="3b1cc-202">`CatalogControllerGetImage`**Should**`.`**Call**`ImageServiceWithId`</span><span class="sxs-lookup"><span data-stu-id="3b1cc-202">`CatalogControllerGetImage`**Should**`.`**Call**`ImageServiceWithId`</span></span>

- <span data-ttu-id="3b1cc-203">`CatalogControllerGetImage`**Should**`.`**Log**`WarningGivenImageMissingException`</span><span class="sxs-lookup"><span data-stu-id="3b1cc-203">`CatalogControllerGetImage`**Should**`.`**Log**`WarningGivenImageMissingException`</span></span>

<span data-ttu-id="3b1cc-204">Algumas equipes consideram a segunda abordagem de nomenclatura mais clara, embora um pouco mais detalhada.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-204">Some teams find the second naming approach clearer, though slightly more verbose.</span></span> <span data-ttu-id="3b1cc-205">De qualquer forma, tente usar uma convenção de nomenclatura que fornece informações sobre o comportamento de teste, de modo que quando um ou mais testes falharem, seja óbvio descobrir, com base nos nomes, quais casos falharam.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-205">In any case, try to use a naming convention that provides insight into test behavior, so that when one or more tests fail, it's obvious from their names what cases have failed.</span></span> <span data-ttu-id="3b1cc-206">Evite nomear os testes de modo vago, como ControllerTests.Test1, pois essa nomenclatura não oferece nenhum valor quando você vê esses nomes em resultados de teste.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-206">Avoid naming you tests vaguely, such as ControllerTests.Test1, as these offer no value when you see them in test results.</span></span>

<span data-ttu-id="3b1cc-207">Se você segue uma convenção de nomenclatura como a mostrada acima, que produz muitas classes de teste pequenas, é uma boa ideia organizar ainda mais os testes usando pastas e namespaces.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-207">If you follow a naming convention like the one above that produces many small test classes, it's a good idea to further organize your tests using folders and namespaces.</span></span> <span data-ttu-id="3b1cc-208">A Figura 9-4 mostra uma abordagem para organizar os testes por pasta dentro de vários projetos de teste.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-208">Figure 9-4 shows one approach to organizing tests by folder within several test projects.</span></span>

![](./media/image9-4.png)

<span data-ttu-id="3b1cc-209">**Figura 9-4.**</span><span class="sxs-lookup"><span data-stu-id="3b1cc-209">**Figure 9-4.**</span></span> <span data-ttu-id="3b1cc-210">Organizando classes de teste por pasta com base na classe que está sendo testada.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-210">Organizing test classes by folder based on class being tested.</span></span>

<span data-ttu-id="3b1cc-211">É claro que, se uma classe de aplicativo específica tiver muitos métodos que estão sendo testados (e, portanto, muitas classes de teste), talvez faça sentido colocá-los em uma pasta correspondente à classe de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-211">Of course, if a particular application class has many methods being tested (and thus many test classes), it may make sense to place these in a folder corresponding to the application class.</span></span> <span data-ttu-id="3b1cc-212">Essa organização não é diferente da forma como você pode organizar arquivos em pastas em outro lugar.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-212">This organization is no different than how you might organize files into folders elsewhere.</span></span> <span data-ttu-id="3b1cc-213">Caso você tenha mais de três ou quatro arquivos relacionados em uma pasta que contém muitos outros arquivos, geralmente, é útil movê-los para sua própria subpasta.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-213">If you have more than three or four related files in a folder containing many other files, it's often helpful to move them into their own subfolder.</span></span>

## <a name="unit-testing-aspnet-core-apps"></a><span data-ttu-id="3b1cc-214">Realizando teste de unidade em aplicativos ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="3b1cc-214">Unit testing ASP.NET Core apps</span></span>

<span data-ttu-id="3b1cc-215">Em um aplicativo ASP.NET Core bem projetado, a maior parte da complexidade e da lógica de negócios será encapsulada em entidades de negócios e uma variedade de serviços.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-215">In a well-designed ASP.NET Core application, most of the complexity and business logic will be encapsulated in business entities and a variety of services.</span></span> <span data-ttu-id="3b1cc-216">O aplicativo ASP.NET Core MVC em si, com seus controladores, filtros, modelos de exibição e exibições, deve exigir muito poucos testes de unidade.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-216">The ASP.NET Core MVC app itself, with its controllers, filters, viewmodels, and views, should require very few unit tests.</span></span> <span data-ttu-id="3b1cc-217">Grande parte da funcionalidade de determinada ação se encontra fora do próprio método de ação.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-217">Much of the functionality of a given action lies outside the action method itself.</span></span> <span data-ttu-id="3b1cc-218">O teste para saber se o roteamento funciona corretamente, ou o tratamento de erro global, não pode ser feito efetivamente com um teste de unidade.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-218">Testing whether routing works correctly, or global error handling, cannot be done effectively with a unit test.</span></span> <span data-ttu-id="3b1cc-219">Da mesma forma, os filtros, incluindo filtros de validação de modelo e autenticação e autorização, não podem ser testados com testes de unidade.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-219">Likewise, any filters, including model validation and authentication and authorization filters, cannot be unit tested.</span></span> <span data-ttu-id="3b1cc-220">Sem essas fontes de comportamento, a maioria dos métodos de ação deve ser insignificantemente pequena, com a delegação da maior parte de seu trabalho para serviços que podem ser testados sem depender do controlador que os usa.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-220">Without these sources of behavior, most action methods should be trivially small, delegating the bulk of their work to services that can be tested independent of the controller that uses them.</span></span>

<span data-ttu-id="3b1cc-221">Às vezes, você precisará refatorar o código para submetê-lo ao teste de unidade.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-221">Sometimes you'll need to refactor your code in order to unit test it.</span></span> <span data-ttu-id="3b1cc-222">Com frequência, isso envolve a identificação de abstrações e o uso da injeção de dependência para acessar a abstração no código que você deseja testar, em vez da codificação direta na infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-222">Frequently this involves identifying abstractions and using dependency injection to access the abstraction in the code you'd like to test, rather than coding directly against infrastructure.</span></span> <span data-ttu-id="3b1cc-223">Por exemplo, considere este método de ação simples para a exibição de imagens:</span><span class="sxs-lookup"><span data-stu-id="3b1cc-223">For example, consider this simple action method for displaying images:</span></span>

```csharp
[HttpGet("[controller]/pic/{id}")]
public IActionResult GetImage(int id)
{
    var contentRoot = _env.ContentRootPath + "//Pics";
    var path = Path.Combine(contentRoot, id + ".png");
    Byte[] b = System.IO.File.ReadAllBytes(path);
    return File(b, "image/png");
}
```

<span data-ttu-id="3b1cc-224">Submeter esse método ao teste de unidade é dificultado por sua dependência direta de `System.IO.File`, que ele usa para ler o sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-224">Unit testing this method is made difficult by its direct dependency on `System.IO.File`, which it uses to read from the file system.</span></span> <span data-ttu-id="3b1cc-225">Você pode testar esse comportamento para garantir que ele funciona conforme esperado, mas fazer isso com arquivos reais é um teste de integração.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-225">You can test this behavior to ensure it works as expected, but doing so with real files is an integration test.</span></span> <span data-ttu-id="3b1cc-226">Vale a pena observar que não é possível submeter a rota desse método a um teste de unidade. Você verá como fazer isso com um teste funcional em breve.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-226">It's worth noting you can't unit test this method's route – you'll see how to do this with a functional test shortly.</span></span>

<span data-ttu-id="3b1cc-227">Se você não pode realizar o teste de unidade no comportamento do sistema de arquivos diretamente e não pode testar a rota, o que há para testar?</span><span class="sxs-lookup"><span data-stu-id="3b1cc-227">If you can't unit test the file system behavior directly, and you can't test the route, what is there to test?</span></span> <span data-ttu-id="3b1cc-228">Bem, depois de fazer a refatoração para possibilitar o teste de unidade, talvez você descubra alguns casos de teste e um comportamento ausente, como o tratamento de erro.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-228">Well, after refactoring to make unit testing possible, you may discover some test cases and missing behavior, such as error handling.</span></span> <span data-ttu-id="3b1cc-229">O que o método faz quando um arquivo não é encontrado?</span><span class="sxs-lookup"><span data-stu-id="3b1cc-229">What does the method do when a file isn't found?</span></span> <span data-ttu-id="3b1cc-230">O que ele deve fazer?</span><span class="sxs-lookup"><span data-stu-id="3b1cc-230">What should it do?</span></span> <span data-ttu-id="3b1cc-231">Neste exemplo, o método refatorado tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="3b1cc-231">In this example, the refactored method looks like this:</span></span>

```csharp
[HttpGet("[controller]/pic/{id}")\]
public IActionResult GetImage(int id)
{
    byte[] imageBytes;
    try
    {
        imageBytes = _imageService.GetImageBytesById(id);
    }
    catch (CatalogImageMissingException ex)
    {
        _logger.LogWarning($"No image found for id: {id}");
        return NotFound();
    }
    return File(imageBytes, "image/png");
}
```

<span data-ttu-id="3b1cc-232">O \_agente e o \_imageService são injetados como dependências.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-232">The \_logger and \_imageService are both injected as dependencies.</span></span> <span data-ttu-id="3b1cc-233">Agora você pode testar se a mesma ID passada para o método de ação é passada para o \_imageService, e se os bytes resultantes são retornados como parte do FileResult.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-233">Now you can test that the same id that is passed to the action method is passed to the \_imageService, and that the resulting bytes are returned as part of the FileResult.</span></span> <span data-ttu-id="3b1cc-234">Você também pode testar se o log de erros ocorre conforme esperado e se um resultado NotFound é retornado caso a imagem esteja ausente, supondo que esse seja um comportamento importante do aplicativo (ou seja, não apenas um código temporário adicionado pelo desenvolvedor para diagnosticar um problema).</span><span class="sxs-lookup"><span data-stu-id="3b1cc-234">You can also test that error logging is happening as expected, and that a NotFound result is returned if the image is missing, assuming this is important application behavior (that is, not just temporary code the developer added to diagnose an issue).</span></span> <span data-ttu-id="3b1cc-235">A lógica real do arquivo foi movida para um serviço de implementação separado e foi aumentada para retornar uma exceção específica do aplicativo para o caso de um arquivo ausente.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-235">The actual file logic has moved into a separate implementation service, and has been augmented to return an application-specific exception for the case of a missing file.</span></span> <span data-ttu-id="3b1cc-236">Você pode testar essa implementação de forma independente, usando um teste de integração.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-236">You can test this implementation independently, using an integration test.</span></span>

<span data-ttu-id="3b1cc-237">Na maioria dos casos, será melhor usar manipuladores de exceção globais em seus controladores, portanto, a quantidade de lógica contida neles será mínima e provavelmente não valerá a pena usar testes de unidade.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-237">In most cases, you’ll want to use global exception handlers in your controllers, so the amount of logic in them should be minimal and probably not worth unit testing.</span></span> <span data-ttu-id="3b1cc-238">Você deve executar a maior parte dos testes de ações do controlador usando testes funcionais e a classe `TestServer` descrita abaixo.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-238">You should do most of your testing of controller actions using functional tests and the `TestServer` class described below.</span></span>

## <a name="integration-testing-aspnet-core-apps"></a><span data-ttu-id="3b1cc-239">Realizando testes de integração em aplicativos ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="3b1cc-239">Integration testing ASP.NET Core apps</span></span>

<span data-ttu-id="3b1cc-240">A maioria dos testes de integração em seus aplicativos ASP.NET Core deve testar serviços e outros tipos de implementação definidos no projeto de infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-240">Most of the integration tests in your ASP.NET Core apps should be testing services and other implementation types defined in your Infrastructure project.</span></span> <span data-ttu-id="3b1cc-241">Por exemplo, você poderia [testar se o EF Core estava atualizando e recuperando com êxito os dados que você espera](https://docs.microsoft.com/ef/core/miscellaneous/testing/) de suas classes de acesso a dados que residem no projeto de infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-241">For example, you could [test that EF Core was successfully updating and retrieving the data that you expect](https://docs.microsoft.com/ef/core/miscellaneous/testing/) from your data access classes residing in the Infrastructure project.</span></span> <span data-ttu-id="3b1cc-242">A melhor maneira de testar se o projeto ASP.NET Core MVC está se comportando corretamente é com testes funcionais executados no aplicativo em execução em um host de teste.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-242">The best way to test that your ASP.NET Core MVC project is behaving correctly is with functional tests that run against your app running in a test host.</span></span>

## <a name="functional-testing-aspnet-core-apps"></a><span data-ttu-id="3b1cc-243">Realizando teste funcional em aplicativos ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="3b1cc-243">Functional testing ASP.NET Core apps</span></span>

<span data-ttu-id="3b1cc-244">Para os aplicativos ASP.NET Core, a classe `TestServer` facilita bastante a escrita de testes funcionais.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-244">For ASP.NET Core applications, the `TestServer` class makes functional tests fairly easy to write.</span></span> <span data-ttu-id="3b1cc-245">Você configura um `TestServer` usando um `WebHostBuilder` diretamente (como faz normalmente com seu aplicativo) ou com o tipo `WebApplicationFactory` (disponível desde a versão 2.1).</span><span class="sxs-lookup"><span data-stu-id="3b1cc-245">You configure a `TestServer` using a `WebHostBuilder` directly (as you normally do for your application), or with the `WebApplicationFactory` type (available since version 2.1).</span></span> <span data-ttu-id="3b1cc-246">Você deve tentar corresponder o host de teste ao host de produção o máximo possível, para que seus testes tenham um comportamento semelhante ao que o aplicativo terá em produção.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-246">You should try to match your test host to your production host as closely as possible, so your tests will exercise behavior similar to what the app will do in production.</span></span> <span data-ttu-id="3b1cc-247">A classe `WebApplicationFactory` é útil para a configuração de ContentRoot do TestServer, que é usada pelo ASP.NET Core para localizar recursos estáticos, como Exibições.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-247">The `WebApplicationFactory` class is helpful for configuring the TestServer's ContentRoot, which is used by ASP.NET Core to locate static resource like Views.</span></span>

<span data-ttu-id="3b1cc-248">Você pode criar testes funcionais simples criando uma classe de teste que implementa IClassFixture\<WebApplicationFactory\<TEntry>>, em que TEntry é a classe de inicialização do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-248">You can create simple functional tests by creating a test class that implements IClassFixture\<WebApplicationFactory\<TEntry>> where TEntry is your web application's Startup class.</span></span> <span data-ttu-id="3b1cc-249">Com isso em vigor, o acessório de teste pode criar um cliente usando o método CreateClient do alocador:</span><span class="sxs-lookup"><span data-stu-id="3b1cc-249">With this in place, your test fixture can create a client using the factory's CreateClient method:</span></span>

```cs
public class BasicWebTests : IClassFixture<WebApplicationFactory<Startup>>
{
    protected readonly HttpClient _client;

    public BaseWebTest(WebApplicationFactory<Startup> factory)
    {
        _client = factory.CreateClient();
    }

    // write tests that use _client
}
```

<span data-ttu-id="3b1cc-250">Geralmente é necessário executar alguma configuração adicional do site antes da execução de cada teste, como configurar o aplicativo para usar um armazenamento de dados na memória e, em seguida, propagar o aplicativo com os dados de teste.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-250">Frequently, you'll want to perform some additional configuration of your site before each test runs, such as configuring the application to use an in memory data store and then seeding the application with test data.</span></span> <span data-ttu-id="3b1cc-251">Para fazer isso, você deve criar sua própria subclasse de WebApplicationFactory\<TEntry> e substituir seu método ConfigureWebHost.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-251">To do this, you should create your own subclass of WebApplicationFactory\<TEntry> and override its ConfigureWebHost method.</span></span> <span data-ttu-id="3b1cc-252">O exemplo a seguir é do projeto FunctionalTests de eShopOnWeb e é usado como parte dos testes no aplicativo Web principal.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-252">The example below is from the eShopOnWeb FunctionalTests project and is used as part of the tests on the main web application.</span></span>

```cs
using Microsoft.AspNetCore.Hosting;
using Microsoft.AspNetCore.Mvc.Testing;
using Microsoft.EntityFrameworkCore;
using Microsoft.eShopWeb.Infrastructure.Data;
using Microsoft.eShopWeb.Infrastructure.Identity;
using Microsoft.eShopWeb.Web;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Logging;
using System;

namespace Microsoft.eShopWeb.FunctionalTests.Web.Controllers
{
    public class CustomWebApplicationFactory<TStartup>
    : WebApplicationFactory<Startup>
    {
        protected override void ConfigureWebHost(IWebHostBuilder builder)
        {
            builder.ConfigureServices(services =>
            {
                // Create a new service provider.
                var serviceProvider = new ServiceCollection()
                    .AddEntityFrameworkInMemoryDatabase()
                    .BuildServiceProvider();

                // Add a database context (ApplicationDbContext) using an in-memory 
                // database for testing.
                services.AddDbContext<CatalogContext>(options =>
                {
                    options.UseInMemoryDatabase("InMemoryDbForTesting");
                    options.UseInternalServiceProvider(serviceProvider);
                });

                services.AddDbContext<AppIdentityDbContext>(options =>
                {
                    options.UseInMemoryDatabase("Identity");
                    options.UseInternalServiceProvider(serviceProvider);
                });

                // Build the service provider.
                var sp = services.BuildServiceProvider();

                // Create a scope to obtain a reference to the database
                // context (ApplicationDbContext).
                using (var scope = sp.CreateScope())
                {
                    var scopedServices = scope.ServiceProvider;
                    var db = scopedServices.GetRequiredService<CatalogContext>();
                    var loggerFactory = scopedServices.GetRequiredService<ILoggerFactory>();

                    var logger = scopedServices
                        .GetRequiredService<ILogger<CustomWebApplicationFactory<TStartup>>>();

                    // Ensure the database is created.
                    db.Database.EnsureCreated();

                    try
                    {
                        // Seed the database with test data.
                        CatalogContextSeed.SeedAsync(db, loggerFactory).Wait();
                    }
                    catch (Exception ex)
                    {
                        logger.LogError(ex, $"An error occurred seeding the " +
                            "database with test messages. Error: {ex.Message}");
                    }
                }
            });
        }
    }
}
```

<span data-ttu-id="3b1cc-253">Os testes podem usar esse WebApplicationFactory personalizado para criar um cliente e, em seguida, fazer solicitações ao aplicativo usando essa instância do cliente.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-253">Tests can make use of this custom WebApplicationFactory by using it to create a client and then making requests to the application using this client instance.</span></span> <span data-ttu-id="3b1cc-254">O aplicativo terá dados propagados que poderão ser usados como parte das asserções do teste.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-254">The application will have data seeded that can be used as part of the test's assertions.</span></span> <span data-ttu-id="3b1cc-255">O teste a seguir verifica se a home page do aplicativo eShopOnWeb é carregada corretamente e inclui uma listagem de produtos que foi adicionada ao aplicativo como parte dos dados de semente.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-255">The following test verifies that the home page of the eShopOnWeb application loads correctly and includes a product listing that was added to the application as part of the seed data.</span></span>

```cs
using Microsoft.eShopWeb.FunctionalTests.Web.Controllers;
using Microsoft.eShopWeb.Web;
using System.Net.Http;
using System.Threading.Tasks;
using Xunit;

namespace Microsoft.eShopWeb.FunctionalTests.WebRazorPages
{
    public class HomePageOnGet : IClassFixture<CustomWebApplicationFactory<Startup>>
    {
        public HomePageOnGet(CustomWebApplicationFactory<Startup> factory)
        {
            Client = factory.CreateClient();
        }

        public HttpClient Client { get; }

        [Fact]
        public async Task ReturnsHomePageWithProductListing()
        {
            // Arrange & Act
            var response = await Client.GetAsync("/");
            response.EnsureSuccessStatusCode();
            var stringResponse = await response.Content.ReadAsStringAsync();

            // Assert
            Assert.Contains(".NET Bot Black Sweatshirt", stringResponse);
        }
    }
}
```

<span data-ttu-id="3b1cc-256">Esse teste funcional emprega a pilha completa do aplicativo ASP.NET Core MVC/Razor Pages, incluindo todos os middlewares, filtros, associadores e outros que possam estar em vigor.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-256">This functional test exercises the full ASP.NET Core MVC / Razor Pages application stack, including all middleware, filters, binders, etc. that may be in place.</span></span> <span data-ttu-id="3b1cc-257">Ele verifica se uma determinada rota ("/") retorna o código de status de êxito esperado e a saída HTML.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-257">It verifies that a given route ("/") returns the expected success status code and HTML output.</span></span> <span data-ttu-id="3b1cc-258">Ele faz isso sem configurar um servidor Web real e, portanto, evita grande parte da fragilidade decorrente do uso de um servidor Web real (por exemplo, problemas com as configurações de firewall).</span><span class="sxs-lookup"><span data-stu-id="3b1cc-258">It does so without setting up a real web server, and so avoids much of the brittleness that using a real web server for testing can experience (for example, problems with firewall settings).</span></span> <span data-ttu-id="3b1cc-259">Em geral, os testes funcionais executados no TestServer são mais lentos do que os testes de integração e de unidade, mas são muito mais rápidos do que os testes que seriam executados na rede em um servidor Web de teste.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-259">Functional tests that run against TestServer are usually slower than integration and unit tests, but are much faster than tests that would run over the network to a test web server.</span></span> <span data-ttu-id="3b1cc-260">Use os testes funcionais para garantir a que pilha de front-end do aplicativo funcione conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-260">You should use functional tests to ensure your application's front-end stack is working as expected.</span></span> <span data-ttu-id="3b1cc-261">Esses testes são úteis principalmente quando você encontra duplicação em seus controladores ou páginas e soluciona a duplicação adicionando filtros.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-261">These tests are especially useful when you find duplication in your controllers or pages and you address the duplication by adding filters.</span></span> <span data-ttu-id="3b1cc-262">O ideal é que essa refatoração não altere o comportamento do aplicativo. Um conjunto de testes funcionais pode verificar isso.</span><span class="sxs-lookup"><span data-stu-id="3b1cc-262">Ideally, this refactoring won't change the behavior of the application, and a suite of functional tests will verify this is the case.</span></span>

> ### <a name="references--test-aspnet-core-mvc-apps"></a><span data-ttu-id="3b1cc-263">Referências – Testar aplicativos ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="3b1cc-263">References – Test ASP.NET Core MVC apps</span></span>
>
> - <span data-ttu-id="3b1cc-264">**Teste no ASP.NET Core**</span><span class="sxs-lookup"><span data-stu-id="3b1cc-264">**Testing in ASP.NET Core**</span></span>  
>   <https://docs.microsoft.com/aspnet/core/testing/>
> - <span data-ttu-id="3b1cc-265">**Convenção de nomenclatura de teste de unidade**</span><span class="sxs-lookup"><span data-stu-id="3b1cc-265">**Unit Test Naming Convention**</span></span>  
>   <https://ardalis.com/unit-test-naming-convention>
> - <span data-ttu-id="3b1cc-266">**Testar EF Core**</span><span class="sxs-lookup"><span data-stu-id="3b1cc-266">**Testing EF Core**</span></span>  
>   <https://docs.microsoft.com/ef/core/miscellaneous/testing/>

>[!div class="step-by-step"]
><span data-ttu-id="3b1cc-267">[Anterior](work-with-data-in-asp-net-core-apps.md)
>[Próximo](development-process-for-azure.md)</span><span class="sxs-lookup"><span data-stu-id="3b1cc-267">[Previous](work-with-data-in-asp-net-core-apps.md)
[Next](development-process-for-azure.md)</span></span>