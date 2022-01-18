# Uma metodologia de modelagem para APIs web

CURTIR[1](https://www.infoq.com/br/articles/web-api-design-methodology/#theCommentsSection)PRINT

18 AGO 2015 18 MIN(S) DE LEITURA

por

- [![img](https://cdn.infoq.com/statics_s1_20211012-0246/images/profiles/HYh2pgO6YuPiaXIfqVsBqK6tdG2bjIyx.jpg)](https://www.infoq.com/br/profile/Mike-Amundsen/)[Mike Amundsen](https://www.infoq.com/br/profile/Mike-Amundsen/)

traduzido por

- [Ivan Salvadori](https://www.infoq.com/br/profile/Ivan-Salvadori/)

Projetar APIs Web vai muito além de URLs, [códigos de status HTTP](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html), cabeçalhos e [payloads](http://pt.wikipedia.org/wiki/Payload). O processo de design é essencialmente a "aparência" da API Web, que assume um papel importante e justifica o esforço empregado. Este artigo esboça, de forma breve, uma metodologia que resulta no design de APIs que se beneficiam das vantagens do HTTP e da Web. A metodologia não está restrita ao HTTP. É possível implementar o mesmo serviço através de WebSockets, XMPP, MQTT, etc, pois grande parte do design da API funcionará da mesma forma. Com isso, a metodologia pode ser utilizada com diversos protocolos, além de proporcionar facilidade para implementações e manutenções futuras.

## Um bom design de APIs vai além de URls, códigos de status, cabeçalhos e payloads

De forma geral, o design de APIs Web se concentra em suas características comuns, tais como o formato de URLs, o uso correto dos códigos de status, métodos e cabeçalhos HTTP, além do design de payloads que contém objetos serializados ou inter-relacionados ([object graphs](https://en.wikipedia.org/wiki/Object_graph)). Essas características são importantes detalhes de implementação. Entretanto, não são muito significantes para o design da API. O verdadeiro significado de design é a forma como as funcionalidades essenciais do serviço são expressas e descritas. O design pode contribuir de forma importante para o sucesso e usabilidade da API Web.

Um bom processo de design ou metodologia define, de forma consistente e replicável, um conjunto de etapas que podem ser empregadas para expor um componente de serviço que executa no lado do servidor em uma API Web acessível e utilizável. Isso significa que uma metodologia pode ser compartilhada entre desenvolvedores, designers e arquitetos de software para auxiliar na coordenação das atividades que constituem um ciclo de implementação. Uma metodologia estabelecida também pode ser refinada ao longo do tempo, à medida que cada equipe descobre maneiras de melhorar e agilizar o processo, sem afetar negativamente os detalhes de implementação. Na verdade, os detalhes de implementação (plataforma, SO, frameworks e GUI) podem mudar independentemente do processo de design, quando claramente separados e definidos.

## Sete etapas de uma metodologia de design de APIs

Este artigo descreve um breve resumo da metodologia de design publicada no livro "[RESTful Web APIs](http://restfulwebapis.com/)" de Richardson e Amundsen. Não é possível apresentar em detalhes todos os passos envolvidos no processo. Entretanto, este artigo apresenta uma visão geral da metodologia. Além disso, este artigo pode ser utilizado como um guia para desenvolver um processo de design específico, adequado às habilidades e objetivos de uma determinada equipe.

*NOTA: Apesar de sete etapas parecer pouco, apenas cinco são destinadas ao design. As outras duas etapas destinam-se à implementação e publicação, complementando o processo para proporcionar uma experiência completa.*

As etapas devem ser seguidas de acordo com a necessidade. É possível avançar para a Etapa 2 (Desenhar diagramas de estados) e perceber que existe mais a ser feito na Etapa 1 (Identificar todas as partes). Ao atingir a Etapa 6 (Iniciar a codificação), pode-se retornar à Etapa 5 (Criar um profile semântico), etc. O mais importante é utilizar a metodologia para apresentar o máximo de detalhes possível, e estar disposto a refazer algumas etapas para complementar os itens que foram deixados para trás. A iteração é fundamental para construir uma visão mais completa dos serviços, e esclarecer como podem ser disponibilizados às aplicações clientes.

### Etapa 1: Identificar todas as partes

A primeira etapa busca identificar todas as informações importantes às aplicações clientes, e disponibilizar através de serviços. Essas informações são denominadas descritores semânticos. A denominação "semântica" está relacionada ao tratamento do significado das informações manipuladas pelas aplicações. A denominação "descritores" é devido ao fato de descrever o comportamento da aplicação propriamente dita. Essas denominações se aplicam sob o ponto de vista da aplicação cliente, e não do servidor. É importante projetar a API como algo que o cliente utilizará. Por exemplo, em uma aplicação simples de lista de tarefas, é possível identificar os seguintes descritores semânticos:

- id : identificador único de cada registro do sistema;
- título : título de cada tarefa;
- prazo : data para completar a tarefa;
- finalizada : flag de sim ou não indicando se a tarefa foi finalizada.

Em uma aplicação completa, podem existir muitos descritores semânticos, como diferentes categorias de listas de tarefas (trabalho, família, jardinagem, etc), informações de usuários (para implementações multi-tenant), dentre outras. A Etapa 1 trata de forma simplificada os descritores semânticos, para dar ênfase ao processo propriamente dito.

### Etapa 2: Desenhar diagramas de estados

A próxima etapa consiste em desenhar diagramas de estados para a API proposta. Cada caixa do diagrama representa uma possível representação. As representações são documentos que possuem um ou mais descritores semânticos identificados na Etapa 1. As setas são utilizadas para indicar as transições entre as representações (de um estado para outro). As transições iniciam-se a partir de requisições do protocolo.

Na Etapa 2 não é necessário estabelecer quais métodos do protocolo serão utilizados em cada transição de estado. Nesta etapa são identificadas apenas se as transições são seguras (HTTP GET), não-seguras/não-idempotentes (HTTP POST) ou não-seguras/idempotentes (HTTP PUT).

*NOTA: Ações idempotentes podem ser executadas repetidas vezes sem causar efeitos inesperados no servidor. Por exemplo, HTTP [PUT](https://tools.ietf.org/html/rfc7231#section-4.3.4) é idempotente porque a especificação diz que os servidores devem utilizar as representações de estado dos recursos, enviadas pelo cliente, para substituir quaisquer valores existentes dos recursos em questão. Entretanto, HTTP [POST](https://tools.ietf.org/html/rfc7231#section-4.3.3) é não-idempotente, pois a especificação HTTP diz que este método deve ser utilizado para adicionar um novo recurso a uma coleção de recursos existente, e não para substituí-lo.*

Nesse caso, uma aplicação cliente para o simples serviço de lista de tarefas, deverá ter acesso à lista de itens disponíveis, ser capaz de filtrar esta lista de itens, obter detalhes de um item específico, além de marcar um item como finalizado. Muitas dessas ações utilizam valores de estado (representações) para passar dados entre cliente e servidor. Por exemplo, a ação de adicionar um novo item permite ao cliente informar os valores de estado "título" e "prazo". A Figura 1 mostra o diagrama de estados da API.

![img](https://imgopt.infoq.com/fit-in/1200x2400/filters:quality(80)/filters:no_upscale()/articles/web-api-design-methodology/pt/resources/1image00.png)

Figura 1: Diagrama de estados.

As ações ilustradas pelo diagrama também são descritores semânticos, pois descrevem os significados das ações para este serviço. Dentre as ações estão:

- ler-lista
- filtrar-lista
- ler-item
- criar-item
- marcar-finalizado

Eventualmente, neste ponto é possível identificar a ausência de ações ou dados importantes para as aplicações clientes. É uma oportunidade para voltar à Etapa 1 e adicionar ou melhorar os descritores no diagrama criado na Etapa 2. Após a revisão das duas primeiras etapas, já se tem uma boa ideia sobre todos os dados e ações que as aplicações clientes necessitam para estabelecer uma interação com o serviço.

### Etapa 3: Conciliar as Strings mágicas

A próxima etapa é [c](http://pt.wikipedia.org/wiki/Strings_mágicas)[onciliar as Strings mágicas](http://pt.wikipedia.org/wiki/Strings_mágicas) da interface do serviço. As Strings mágicas são os nomes dos descritores. Os descritores não possuem significado explícito, eles apenas representam ações ou elementos de dados que serão acessado por aplicações clientes durante a comunicação do serviço. Conciliar os nomes dos descritores implica na adoção de termos conhecidos, provenientes de fontes como:

- [Schema.org](http://schema.org/)
- [microformats.org](http://microformats.org/)
- [Dublin Core](http://dublincore.org/documents/dces/)
- [IANA Link Relation Values](http://www.iana.org/assignments/link-relations/link-relations.xhtml)

Os exemplos citados são repositórios de termos bem definidos e compartilhados. Ao utilizar os termos dessas fontes na interface do serviço, é provável que desenvolvedores tenham conhecimento e entendimento sobre seus significados. Isto pode aumentar a usabilidade da API.

*NOTA: Apesar de utilizar termos compartilhados para os descritores na interface do serviço seja uma boa ideia, não é necessário utilizá-los internamente na implementação, como em nomes dos campos do banco de dados, por exemplo. O próprio serviço pode realizar o mapeamento dos nomes das interfaces publicas com os nomes armazenados internamente sem nenhum problema.*

No exemplo do serviço da lista de tarefas, foi possível associar todos os descritores semânticos com termos existentes, com exceção de "criar-item". Para este caso, foi criado uma URI única, com base nas regras estabelecidas pela [Web Linking RFC5988](https://tools.ietf.org/html/rfc5988). Existem algumas desvantagens ao utilizar termos compartilhados para descrever os descritores da interface. Por exemplo, os termos raramente combinam perfeitamente com os elementos internos da base da dados. Entretanto, essa desvantagem não inviabiliza o uso de termos bem definidos e compartilhados. Dessa forma, obtém-se os seguintes resultados:

- id -> [identifier do Dublin Core](http://purl.org/dc/elements/1.1/identifier)
- título - [name do Schema.org](https://schema.org/name)
- prazo -> [scheduledTime do Schema.org](https://schema.org/scheduledTime)
- finalizado -> [status do Schema.org](https://schema.org/status)
- ler-lista -> [collection do IANA Link Relation Values](http://www.iana.org/assignments/link-relations/link-relations.xhtml)
- filtrar-lista -> [search do IANA Link Relation Values](http://www.iana.org/assignments/link-relations/link-relations.xhtml)
- ler-item -> [item do IANA Link Relation Values](http://www.iana.org/assignments/link-relations/link-relations.xhtml)
- criar-item -> http://mamund.com/rels/create-item using RFC5988
- marcar-finalizado - [edit do IANA Link Relation Values](http://www.iana.org/assignments/link-relations/link-relations.xhtml)

A figura 2 mostra a atualização do diagrama de estados após a conciliação de nomes.

![img](https://imgopt.infoq.com/fit-in/1200x2400/filters:quality(80)/filters:no_upscale()/articles/web-api-design-methodology/pt/resources/1image01.png)

Figura 2: Atualização do diagrama de estados

### Etapa 4: Escolher um formato de dados

A próxima etapa do processo de modelagem de uma API é a escolha de um formato de dados para ser utilizado na troca de mensagens entre cliente e servidor. Uma das características da Web é a transferência de dados em forma de documentos padronizados, através de uma interface uniforme. É importante escolher um formato capaz de suportar os descritores de dados (identificadores e status) bem como os descritores de ação, como, por exemplo: "pesquisar", "editar", etc. Existem poucos formatos disponíveis. Alguns dos mais importantes formatos com suporte hipermídia (sem ordem de importância) são:

- HyperText Markup Language ([HTML](http://www.w3.org/TR/html5/))
- Hypertext Application Language ([HAL](http://stateless.co/hal_specification.html))
- Collection+JSON ([Cj](http://amundsen.com/media-types/collection/))
- [Siren](https://github.com/kevinswiber/siren/blob/master/README.md)
- [JSON-API](http://jsonapi.org/)
- Uniform Basis for Exchanging Representations ([UBER](http://g.mamund.com/uber))

É importante escolher um formato de dados adequado para o protocolo utilizado pela API. A maioria dos desenvolvedores preferem o protocolo [HTTP](https://tools.ietf.org/html/rfc7230) para a interface do serviço. Entretanto, [WebSockets](https://tools.ietf.org/html/rfc6455), [XMPP](http://xmpp.org/rfcs/rfc6120.html), [MQTT](http://public.dhe.ibm.com/software/dw/webservices/ws-mqtt/mqtt-v3r1.html) e [CoAP](https://tools.ietf.org/html/rfc7252) também podem ser utilizados, especialmente para alto desempenho, mensagens curtas e implementações peer-to-peer.

Neste exemplo, o formato utilizado para as mensagens é o HTML, e o protocolo utilizado é o HTTP. O formato HTML possui todos os descritores de dados necessários, como por exemplo *<UL>* para listas, *<LI>* para itens e *<SPAN>* para elementos de dados. O HTML também possui suporte adequado para os descritores de ação, como por exemplo *<A>* para links seguros (somente leitura), *<FORM method="get">* para transições seguras (somente leitura) e *<FORM method="post">* para transições que alteram o estado do recurso, ou seja, transições inseguras.

*NOTA: O diagrama de estados mostra a ação "editar" como idempotente, HTTP PUT por exemplo. Entretanto, o HTML não possui suporte nativo para o PUT. Neste exemplo, utiliza-se um campo adicional para auxiliar o HTML com o suporte para POST-only idempontente.*

Com isso, é possível testar a interface criando alguns exemplos de representação com base no diagrama de estados. Para este exemplo existem apenas duas representações: "Lista de tarefas" e "Item/tarefa" apresentadas nos códigos 1 e 2, respectivamente.

**Código 1: Representando uma coleção de itens a fazer em HTML**

```
<html>
  <head>
    <!-- apenas para teste de apresentação -->
    <title>Lista de tarefas</title>
    <style>
      .name, .scheduledTime, .status, .item {display:block}
    </style>
  </head>
  <body>
      <!-- apenas para teste de apresentação -->
      <h1>Lista de tarefas</h1>
      <!-- coleção de itens -->
      <ul>
        <li>
          <a href="/list/1" rel="item">
            <span>1</span>
          </a>
          <span>Primeiro item da lista</span>
          <span>2014-12-01</span>
          <span>Pendente</span>
        </li>
        <li>
          <a href="/list/2" rel="item">
            <span>2</span>
          </a>
          <span>Segundo item da lista</span>
          <span>2014-12-01</span>
          <span>Pendente</span>
        </li>
        <li>
          <a href="/list/3" rel="item">
            <span>3</span>
          </a>
          <span>Terceiro item da lista</span>
          <span>2014-12-01</span>
          <span>Completo</span>
        </li>
      </ul>
      <!-- transição para procura -->
      <form method="get" action="/list/">
        <legend>Pesquiisa</legend>
        <input />
        <input type="submit" value="Pesquisar nomes" />
      </form>
      <!-- transição de criação para um item -->
      <form method="post" action="/list/" class=">
        <legend>Criar item</legend>
        <input />
        <input />
        <input type="submit" value="Criar item" />
      </form>
  </body>
</html>
```

**Código 2: Representação da coleção de tarefas em HTML**

```
<html>
  <head>
    <!-- apenas para teste de apresentação -->
      <title>Lista de tarefas</title>
      <style>
        .name, .scheduledTime, .status, .item, .collection {display:block}
      </style>
  </head>
  <body>
    <!-- apenas para teste de apresentação -->
    <h1>Item para fazer</h1>
    <a href="/list/" rel="collection">Voltar para a lista</a>
    <!-- coleção de itens de tarefa -->
      <ul>
        <li>
          <a href="/list/1" rel="item">
            <span>1</span>
          </a>
          <span>Primeiro item da lista</span>
          <span>2014-12-01</span>
          <span>Pendente</span>
        </li>
      </ul>
      <!-- transição de edição -->
      <form method="post" action="/list/1">
        <legend>Atualizar status</legend>
        <input type="hidden" value="q1w2e3r4t5y6" />
        <input type="text" value="pending" />
        <input type="submit" value="Atualizar" />
      </form>
  </body>
</html>
```

Lembre-se, através das amostras das representações do diagrama de estados, é possível identificar informações que deveriam estar presentes em decorrência das etapas anteriores (falta de descritores, mudança de descritores de ação, idempotência por exemplo). Este é um bom momento para realizar as correções, antes de transformar o design em código. Isto é, antes de iniciar a codificação, é preciso executar um passo adicional, criar um Profile Semântico**.**

### Etapa 5 : Criar um profile semântico

Um profile semântico é um documento que contém todos os descritores da modelagem da API. O Profile possui detalhes que auxiliam os desenvolvedores nas implementações de aplicações clientes e também de servidores. O Profile é um guia de implementação, não é uma descrição da implementação. Esta distinção é importante.

## Formatos de descrição de serviços

Documentos para descrição de serviços são utilizados há bastante tempo, pois são úteis na geração de código fonte ou para documentar a implementação de um serviço existente. Dentre as principais opções de formatos estão:

- Web Service Definition Language ([WSDL](http://www.w3.org/TR/wsdl))
- Atom Service Description ([AtomSvc](https://tools.ietf.org/html/rfc5023#section-8))
- Web Application Description Language ([WADL](http://www.w3.org/Submission/wadl/))
- [Blueprint](https://github.com/apiaryio/api-blueprint/blob/master/API Blueprint Specification.md)
- [Swagger](https://github.com/wordnik/swagger-spec/blob/master/README.md)
- RESTful Application Modeling Language ([RAML](http://raml.org/spec.html))

## Formatos de profiles

Existem poucas opções de formatos de profile até o momento. Os formatos recomendados são:

- Application-Level Semantic Profiles ([ALPS](http://tools.ietf.org/html/draft-amundsen-richardson-foster-alps-00))
- [JSON-LD](http://www.w3.org/TR/json-ld/) + [Hydra](http://www.hydra-cg.com/)

As duas opções de formatos de profile são relativamente novas. O [JSON-LD](http://www.w3.org/TR/json-ld/) alcançou o status de recomendação do W3C no inicio de 2014. O [Hydra](http://www.w3.org/ns/hydra/spec/latest/core/) continua ainda como um documento não oficial, entretanto, possui uma comunidade ativa de desenvolvedores. O [ALPS](https://tools.ietf.org/html/draft-amundsen-richardson-foster-alps-00) está no estágio inicial de rascunho pelo IETF.

Enquanto a ideia de um documento de profile é descrever os aspectos reais de um determinado problema (não somente uma implementação), o formato de profile é bem diferente dos formatos de descrição típicos.

**Código 3 - Profile semântico da lista para fazer em ALPS:**

```
<alps version="1.0">
  <doc>
        Perfil ALPS para artigo do InfoQ sobre "Modelagem de APIs para Web"
  </doc>
  <!-- descritores de dados -->
  <descriptor type="semantic" ref=" />
  <descriptor type="semantic" ref=" />
  <descriptor type="semantic" ref=" />
  <descriptor type="semantic" ref=" />
  <!-- descritores de ações -->
  <descriptor type="safe" ref=" />
  <descriptor type="safe" ref=" />
  <descriptor href="#identifier" />
  </descriptor>
  <descriptor type="safe" ref=">
        <descriptor href="#name" />
  </descriptor>
  <descriptor id="create-item" type="unsafe" ref=">
        <descriptor href="#name" />
        <descriptor href="scheduledTime" />
  </descriptor>
  <descriptor type="idempotent" ref=">
        <descriptor href="#identifier" />
        <descriptor href="#status" />
  </descriptor>
</alps>
```

Os documentos de profile são semelhantes a vocabulários básicos para todos os possíveis valores e ações da interface de serviço da Lista de Tarefas. Serviços que obedecem a este profile podem tomar suas próprias decisões sobre o protocolo, formato de mensagem e até mesmo URLs. Clientes que aceitam este profile serão desenvolvidos para reconhecer os descritores apresentados no documento. Caso seja apropriado, os descritores reconhecidos podem ser ativados.

Os documentos de profiles também são excelentes para a geração de documentação, que pode ser facilmente lida por seres humanos, para a análise de profiles semelhantes, identificação de profiles comumente usados, e até mesmo para a geração de diagramas de estado.

Ao conciliar os nomes de toda a lista de descritores, revisar o diagrama de estados e o documento de profile semântico, é hora de iniciar a codificação de exemplo de um servidor e um cliente.

### Etapa 6: Iniciar a codificação

Neste ponto, é possível disponibilizar os documentos de modelagem da API (diagrama de estados e o profile semântico) para iniciar a codificação do serviço que será executado no servidor, e das aplicações clientes.

O servidor HTTP deve implementar o diagrama de estados criado na Etapa 2, e as requisições dos clientes devem acionar as transições de estado adequadas no serviço. Cada representação enviada pelo serviço deve utilizar o formato definido na Etapa 3, e deve incluir um link para o profile criado na Etapa 4. As respostas devem incluir os controles hipermídia apropriados, que implementam as ações mostradas no diagrama de estados e descritos no documento de profile. Neste momento, desenvolvedores de serviços que são executados no servidor e desenvolvedores de aplicações clientes, podem realizar implementações de forma relativamente independente, além de executar testes para validar a conformidade com diagrama de estados e com o profile. Ao atingir a estabilidade do código em execução, deve executar a última etapa da metodologia: publicar a API.

### Etapa 7: Publicar a API

APIs Web devem disponibilizar ao menos uma URL capaz de sempre responder as requisições dos clientes, mesmo que não implementada imediatamente. Essa URL é conhecida como "URL billboard", sendo esta URL de conhecimento de todos. É uma boa ideia publicar o documento de profile para que novas implementações do serviço possam ser relacionadas com suas respectivas respostas. É possível também publicar uma documentação legível a seres humanos, no formato de tutoriais, etc, para auxiliar o entendimento dos desenvolvedores de aplicações clientes, na correta utilização dos serviços disponibilizados.

Com a execução das etapas anteriormente citadas, foi modelado um serviço estável, acessível, disponível e pronto para ser utilizado.

## Conclusão

Este artigo abordou um conjunto de etapas para a modelagem de APIs Web. O foco está na descrição e documentação correta dos dados e ações, de forma legível a outras aplicações (*machine-readable*), com o objetivo de facilitar a implementação de serviços e de aplicações clientes, mesmo quando não existe contato direto entre os desenvolvedores. As etapas que compõem a modelagem são:

1. **Identificar todas as partes**
   Reunir todos os elementos de dados de interesse das aplicações clientes para permitir a interação com o serviço.
2. **Desenhar diagramas de estados**
   Documentar todas as ações (transições de estado) disponíveis para o serviço.
3. **Conciliar as Strings mágicas**
   Utilizar (o máximo possível) termos bem conhecidos na interface pública do serviço.
4. **Escolher um formato de dados**
   Encontrar um formato de mensagem que melhor se adapta às transições do serviço com o protocolo utilizado pela API.
5. **Criar um Profile Semântico**
   Escrever um documento de profile que defina todos os descritores utilizados no serviço.
6. **Iniciar a codificação**
   Compartilhar o documento de profile e o diagrama de estados com os desenvolvedores dos serviços do lado servidor e com os desenvolvedores das aplicações clientes, além de iniciar a codificação de testes de aderência ao profile e ao diagrama de estados. Por fim, realizar ajustes caso necessário.
7. **Publicar a API**
   Publicar a "URL billboard" e o documento de profile para que outros possam utilizá-los para criar novos serviços ou aplicações clientes.

É provável que seja preciso revisitar algumas etapas ao descobrir a falta de alguns elementos, e tomar decisões sobre a modelagem. Quanto antes forem identificadas as incoerências, melhor é o processo de desenvolvimento. Além disso, é possível utilizar posteriormente a modelagem da API para implementações que utilizam novos formatos e protocolos solicitados por desenvolvedores.

A metodologia apresentada é apenas uma maneira de desenvolver um processo seguro, reproduzível e consistente, para a modelagem de APIs Web. Ao explorar este exemplo, é possível encontrar pontos de melhorias para situações específicas, como adicionar etapas adicionais ou não executar algumas etapas apresentadas. Além disso, o formato das mensagens e o protocolo poder variar de um caso para outro. Com isso, espera-se proporcionar algumas ideias para criar a melhor metodologia de modelagem de APIs possível para organizações ou times de desenvolvimento.

### Sobre o autor

![img](https://imgopt.infoq.com/fit-in/1200x2400/filters:quality(80)/filters:no_upscale()/articles/web-api-design-methodology/pt/resources/2image03.jpg)**Mike Amundsen** é arquiteto chefe de APIs da Layer7 Technologies, auxilia pessoas a construir boas APIs para a Web. Autor e palestrante internacionalmente conhecido, Mike viaja por todo os Estados Unidos e Europa, executando consultorias e palestras sobre arquitetura distribuída, desenvolvimento de aplicações Web, computação em nuvem e outros assuntos. Mike possui dezenas de livros com a sua autoria.