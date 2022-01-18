# Arquitetando uma API RESTful

[![Ramon Lacava Gutierrez Gonçales](https://miro.medium.com/fit/c/56/56/2*c3kvfLCs_w316UqlmOLHFQ.jpeg)](https://medium.com/@ramonrune?source=post_page-----8ffcf892586a--------------------------------)

[Ramon Lacava Gutierrez Gonçales](https://medium.com/@ramonrune?source=post_page-----8ffcf892586a--------------------------------)

[Nov 3, 2019·19 min read](https://medium.com/@ramonrune/arquitetando-uma-api-restful-8ffcf892586a?source=post_page-----8ffcf892586a--------------------------------)







![img](https://miro.medium.com/max/1252/0*ebVHI6G5KAWo8Rzt.jpg)

# Sumário

1. Uma breve introdução ao REST.
2. Uma breve introdução ao HTTP.
3. Conceitos importantes para uma API RESTful.
4. Melhores práticas para o Design de uma API RESTful.
5. Linguagens de programação e plataformas para publicar as APIs
6. Agradecimentos

**Objetivo**: Apresentar melhores práticas no Design de APIs RESTful, exemplos de APIs reais em diferentes linguagens de programação, preços para execução, e muito mais!

# 1. Uma breve introdução ao REST

As APIs de serviços web tem cada vez crescido mais, permitindo empresas expandirem negócios, fornecendo integrações a diversos serviços. Sem dúvidas isso acaba gerando efeitos tanto nos negócios quanto na área técnica. Existem diversas APIs criadas a partir do conceito **REST (Representational State Transfer),** o qual define um conjunto de princípios arquiteturais para a comunicação entre cliente e servidor. REST foi criado por Roy Fielding em sua Tese de Doutorado. Roy Fielding também é conhecido por ser um dos autores do protocolo **HTTP.** Vale notar que REST não tem uma relação obrigatória com o HTTP, embora o mercado utilize REST e HTTP amplamente.

O **REST** se baseia em diversos princípios, tais como:

- Baseia-se no estilo arquitetural **cliente** e **servidor**, o que permite portabilidade da interface do usuário em múltiplas plataformas e auxilia na **escalabilidade**. Um cliente realiza requisições para um servidor, o qual processa os dados, e fornece uma resposta ao cliente.
- **Stateless (ausência de estado)**, ou seja, cada requisição do cliente ao servidor deve ter todas as informações necessárias para que o servidor entenda a requisição.
- Possibilidade de suporte a **cache para otimizar a eficiência da rede.**
- **Interface uniforme** de acesso por parte do servidor para que diferentes clientes interajam de forma facilitada com o servidor.

Para compreender o REST, também temos que compreender os seguintes elementos:

- **Recurso**: O Alvo/Objetivo conceitual pretendido. Pode ser um documento, imagem, coleção de outros recursos, etc.
- **Identificador de recurso**: Recursos devem estar presentes e serem acessíveis de alguma maneira, tais como URL, URN, etc.
- **Representação**: Define como o recurso é representado, se é uma imagem PNG, JPEG, um documento HTML, CSS, etc. Conta também com meta dados da representação, como ultima data de modificação, etc.
- **Dados de controle**: Dados a fins de controle de cache, etc.

# 2. Uma breve introdução ao HTTP

O protocolo HTTP é amplamente utilizado em conjunto com o REST. No HTTP, a comunicação se da entre o cliente e o servidor através de **requisições** e **respostas**. A imagem a seguir apresenta uma requisição feita de um navegador para um servidor Web.

![img](https://miro.medium.com/max/60/0*A51GZQlSd9BWCRv5.png?q=20)

![img](https://miro.medium.com/max/590/0*A51GZQlSd9BWCRv5.png)

Note os seguintes elementos de uma requisição:

## 2.1 Método

Os métodos (GET, POST, PUT, DELETE, PATCH,etc ) permitem manipular os recursos em servidores web.

- **GET**: É utilizado para operações de leitura de recursos.
- **DELETE**: É utilizado para operações de remoção de recursos.
- **POST**: Geralmente utilizado para criar um novo recurso.*
- **PUT:** Geralmente utilizado para atualização de um recurso. *

***ATENÇÃO! Quando não sabemos a localização de um novo recurso, devemos utilizar POST, e quando sabemos a localização de um recurso, o método PUT! Na definição do HTTP não há nada que associe POST a inserir e PUT a atualizar, embora o mesmo seja utilizado para estes fins normalmente.**

## 2.2 Endereço do recurso

Para realizar a manipulação de dados é necessário saber onde está localizado o endereço do recurso. Em uma analogia, pense em uma rua. Você vai até um determinado endereço de uma casa (endereço) a fim de realizar alguma operação (método).

## 2.3 Versão do protocolo HTTP.

Indica a versão do protocolo HTTP que está sendo utilizada na comunicação. Pode ser utilizado HTTP 1.1, 2.0, etc.

## 2.4 Cabeçalhos

Estrutura de chave e valor. Incluem o host, tamanho do conteúdo, formatos aceitos, linguagens aceitas, etc.

## 2.5 Corpo da requisição.

Podemos utilizar diversos formatos:

- **None:** Não há um corpo para a requisição.
- **Form-data**: São enviados a partir de estrutura de chave e valor. Por exemplo: chave: usuario, valor: Usuario De Teste. Cada par é uma parte da mensagem e tem seu próprio cabeçalho.
- **Xwww-form-urlencoded:** Separa chave e valor em chaves. Por ex: nome=teste&idade=25
- **Raw**: Formato “cru”, pode ser enviado texto, JSON, XML, HTML, JavaScript, etc.
- **Binary:** Utilizado para recursos em formato binário. Por exemplo: Enviar arquivos PDF, etc.

Com tudo isto definido, a **mensagem** é enviada do **cliente** para o **servidor**, o **servidor a processa e envia de volta uma resposta ao cliente**, de maneira semelhante a da imagem abaixo.

![img](https://miro.medium.com/max/60/0*0fi6FsOgAkmNxwrw.png?q=20)

![img](https://miro.medium.com/max/630/0*0fi6FsOgAkmNxwrw.png)

Podemos notar novamente a versão do protocolo (HTTP/1.1), cabeçalhos de resposta, corpo de resposta (pode ser HTML, JSON, XML,etc). Porem há um elemento novo, o **Status da Resposta com um descritivo**.

## 2.6 Código de status da resposta

Indica se a requisição foi concluída de maneira correta. Existem cinco classificações de respostas, as de **informação, sucesso, redirecionamento, erro do cliente e erro do servidor.**

- **De 100 a 199**: Respostas de informação. Ex: 102 PROCESSING — diz que o servidor já recebeu a requisição mas nenhuma resposta está disponível no momento.
- **De 200 a 299:** Respostas de sucesso. Ex: 200 OK — Requisição bem sucedida. 201 CREATED — Novo recurso criado (utilizado em requisições POST por exemplo).
- **De 300 a 399:** Respostas de redirecionamento. Ex: 302 FOUND — Significa que a URI do recurso foi mudada temporariamente.
- **De 400 a 499:** Respostas de erro do cliente. Ex: 404 NOT FOUND — Recurso não encontrado. 401 UNAUTHORIZED- Cliente deve se autenticar. 400 BAD REQUEST. — Servidor não entendeu a requisição dado alguma sintaxe inválida.
- **Acima de 500:** Respostas de erro no servidor. Ex: 500 INTERNAL SERVER ERROR — Servidor encontrou uma situação que ele não sabe lidar. 503 SERVICE UNAVAILABLE — Servidor não está pronto para manipular a requisição, o serviço está indisponível.

# 3. Conceitos importantes para uma API Restful

Agora iremos abordar um pouco sobre diversos conceitos importantes no mundo REST.

## 3.1 Modelando pensando em Idempotência e segurança

Antes de iniciar a modelagem de uma API Restful, é necessário sabermos alguns conceitos sobre **idempotência e segurança**. Ambos estes conceitos estão relacionados diretamente aos métodos HTTP. Note que **a modelagem de forma correta destes conceitos é de grande importância**, pois, alem de **prevenir possíveis problemas e efeitos indesejados**, acaba gerando um **mecanismo padrão a ser seguido por toda a equipe de desenvolvimento**.

![img](https://miro.medium.com/max/60/0*DpdbJdENtF_LuaNM.png?q=20)

![img](https://miro.medium.com/max/328/0*DpdbJdENtF_LuaNM.png)

## 3.1.1 Métodos seguros

Um método é tido como seguro **se ele for utilizado apenas para operações de leitura**, tais como o GET, HEAD e OPTIONS. **Não se espera que seja feito qualquer tipo de alteração no estado do servidor ao realizar uma requisição a estes métodos.**

De acordo com a definição da RFC 2616:

> In particular, the convention has been established that the GET and HEAD methods SHOULD NOT have the significance of taking an action other than retrieval. These methods ought to be considered “safe”. This allows user agents to represent other methods, such as POST, PUT and DELETE, in a special way, so that the user is made aware of the fact that a possibly unsafe action is being requested. RFC 2616 Fielding, et al.

## 3.1.2 Métodos Idempotentes

De acordo com a definição original definida na RFC 7231:

> A request method is considered “idempotent” if the intended effect on the server of multiple identical requests with that method is the same as the effect for a single such request. RFC 7231 Seção 4.2.2. Fielding & Reschke.

Em linhas gerais, **um método é considerado idempotente se os efeitos colaterais de uma ou mais requisições idênticas forem iguais a uma única requisição**.

**Idempotência se refere ao estado do sistema depois que a requisição tenha sido completada.** Logo, caso você faça uma operação que envolve o método DELETE para remover algo, após a remoção, o recurso não existe mais no servidor. Agora, independente da quantidade de vezes que você executar a mesma requisição DELETE, o servidor continuará com mesmo estado. Logo, DELETE é um método idempotente. O mesmo conceito pode se aplicar aos métodos GET, PUT, HEAD e OPTIONS, seguindo a linha de raciocínio do método DELETE.

**Note que durante essas requisições, o servidor pode responder de maneira diferente, porem, o estado do servidor continua o mesmo.**

## 3.2 Modelando pensando no Modelo de Maturidade de Richardson.

É muito comum encontrar definições do modelo de maturidade de Richardson sendo algo como: **Os passos para se alcançar a glória do REST**. O modelo de Richardson basicamente divide o REST em três passos que introduzem recursos, métodos HTTP e Hypermedia.

![img](https://miro.medium.com/max/60/0*TJCnow0Iq8NInxbb.png?q=20)

![img](https://miro.medium.com/max/606/0*TJCnow0Iq8NInxbb.png)

A divisão se dá por quatro níveis na realidade. Nível 0, 1, 2 e 3.

## 3.2.1 O nível 0 — Pantano

No nível 0, é o conhecido **pântano**, onde **não se utiliza múltiplos endereços para recursos, não há diferenciação entre os métodos HTTP, Status do código de resposta, nem nada disso**. O que existe basicamente é uma chamada remota.

Um exemplo disso é realizar requisições a um único endereço, e dependendo do corpo da mensagem que for enviado, o servidor realizará uma ação específica. É extremamente difícil de ser mantido.

## 3.2.2 O nível 1 — Recursos

No nível 1, as coisas começam a ficar mais divididas. Se começa a utilizar o conceito de recursos, então, ao invés de enviar todas as requisições a um único endereço, agora chamamos endereços individuais.

Um exemplo, é existirem vários endpoints ao invés de um único endpoint (como no nível 1). Como por exemplo:

- http://servidor.com/clientes
- http://servidor.com/pagamentos

Isso acaba gerando uma melhor divisão de conceitos, o que facilita a gestão dos recursos.

## 3.2.3 O nível 2 — Métodos e Status HTTP

Para estar neste nível, o pré-requisito é o nível 1. Já para estar no nível 2, é necessário utilizar os métodos HTTP e os códigos de status de maneira correta. Utilizar GET para obter dados, DELETE para remover, POST quando não se sabe o endereço do recurso (tipicamente adicionar), PUT quando se sabe o endereço do recurso (tipicamente alterar).

Um exemplo disso, é o seguinte caso: Imagine enviar uma requisição para o nosso antigo serviço http://servidor.com/clientes. Digamos que iremos utilizar uma POST para adicionar um novo cliente. Logo, no final da requisição, o código de retorno deve ser 201 — CREATED. Ao consultar um recurso que não existe, retornar 404 — NOT FOUND. Em casos de falta de autenticação, utilizar 401 — UNAUTHORIZED. Se não se pode realizar uma ação especifica devido a algumas regras, 403 — FORBIDDEN.

## 3.2.4 O nível 3 — Controles de Hypermedia

Aqui o pré-requisito é já estar no nível 2 de maturidade. O nível 3 é o chamado “A glória do REST”.

No nível 3, introduzimos os controles de hypermedia. Você já deve ter ouvido falar de HATEOS (Hypertext As The Engine Of Application State). É basicamente a capacidade de “navegar” de uma API para outra através de recursos de Hyper Media.

Assim como citado por Martin Fowler, este seria um possível retorno de uma API nível 3:

> GET /doctors/mjones/slots?date=20100104&status=open HTTP/1.1
> Host: royalhope.nhs.uk
>
> HTTP/1.1 200 OK
> [various headers]
>
> <openSlotList>
> <slot id = “1234” doctor = “mjones” start = “1400” end = “1450”>
> <link rel = “/linkrels/slot/book”
> uri = “/slots/1234”/>
> </slot>
> <slot id = “5678” doctor = “mjones” start = “1600” end = “1650”>
> <link rel = “/linkrels/slot/book”
> uri = “/slots/5678”/>
> </slot>
> </openSlotList>

Note a capacidade de navegar entre APIs facilmente. Por exemplo, uma API de listagem de clientes poderia retorna Links para APIs de pagamentos específicas para cada cliente.

**Por definição, na tese de Roy Fielding, para uma API ser considerada REST ela deve estar no nível 3**. Porem, no dia a dia das empresas nem sempre uma API RESTful necessita estar no nível 3. Praticar algo em torno do nível 2 e nível 3 já está de bom tamanho!

# 4. Melhores práticas para o Design de uma API RESTful

Ao realizar o design de uma API RESTful, devemos entender que ela será um serviço exposto para um desenvolvedor, então devemos colocar esforços em tornar nossa API apresentável. Vamos apresentar algumas boas práticas no mundo das APIs.

## 4.1 Use recursos corretamente

**Um recurso deve ser um substantivo, e não um verbo**! Por exemplo, ao envés de:

- GET /listar_clientes — **Errado**
- GET /clientes — **Certo**

Algumas pessoas preferem utilizar o substantivo no plural, outras no singular. Isso não importa, o importante é que você deve **seguir um padrão** em todas as suas APIs, então, se modelar um recurso semelhante a GET /clientes, sempre utilize plural. O importante é a padronização. Escolha se irá utilizar substantivos no plural ou singular e **aplique em seu projeto de forma consistente**.

Outra observação é que **recursos devem ser descritivos, fáceis de entender, e para isso, é recomendado utilizar o nível 2 ou nível 3 de maturidade de Richardson.** Por exemplo:

- GET /clientes — Lista os clientes.
- GET /clientes/1 — Obtém os dados do cliente 1.
- POST /clientes — Cria um novo cliente.
- PUT /clientes/1 — Altera o cliente 1.
- DELETE /clientes/1 — Remove o cliente 1.
- PATCH /clientes/1 — Atualiza parcialmente o cliente 1.

Também podemos realizar relações de recursos, tais como:

- GET /clientes/1/parceiros — Lista os parceiros do cliente 1.
- GET /clientes/1/parceiros/1 — Lista o parceiro 1 do cliente 1.

Note que devemos tomar cuidado com a extensão do recurso. Utilize normalmente no máximo um encadeamento de 3–4 recursos no máximo. Isso para facilitar a compreensão.

## 4.2 Documente sua API

Algumas pessoas dizem que uma API é tão boa quanto sua documentação. A documentação precisa ser fácil de encontrar, compreensível ao desenvolvedor, fácil de testar e informar o seu proposito específico.

Um bom exemplo a ser seguido é a API da Marvel (acesso a ela nas referências). Ela possui uma lista das APIs, o método, recurso e uma descrição simples do que ela faz. Ao clicar em uma API em específico, temos uma descrição, os dados que a API retorna e possíveis códigos de status que o servidor pode retornar.

Também é muito interessante fornecer ao desenvolvedor um ambiente em que ele possa simular a API. Em casos de API muito complexas, como por exemplo, emissão de uma nota fiscal, lidar com dados bancários, etc, é bom termos um manual de referência muito bem documentados e atualizados para facilitar a vida do desenvolvedor.

## 4.3 Versione sua API e dê significados a ela

**É uma boa prática sempre versionar sua API**. Normalmente se utiliza o versionamento na URI do recurso:

- GET /v1/clientes
- POST /v1/clientes

Também podemos criar uma nomenclatura própria dependendo da demanda interna da API. Por exemplo, em um conjunto de APIs que estarão disponíveis para o público em geral, podemos utilizar a seguinte nomeação:

- GET /v1/public/characters
- GET/v1/public/characters/1

Este é o modelo utilizado pela API da Marvel, o qual é extremamente descritivo e intuitivo.

## 4.4 Utilize JSON onde conseguir para a resposta de suas APIs

Sabemos que em alguns casos específicos precisamos lidar com XML. Porem, **onde for possível, realize a resposta de suas APIs em formato JSON**. Além de ser um formato amplamente utilizado na Web, **os arquivos JSON usam 30% menos banda do que arquivos XML**.

Nos campos do JSON, existem desenvolvedores que usam Camel Case (camelCase) e snake case (snake_case). Não existe certo ou errado, porem, novamente, é importante seguir um padrão e manter a consistência. Uma dica interessante apresentada no artigo de Vinay Shani (pode ser visto em referencias) é **utilizar a convenção da linguagem** que você está usando. Exemplo: Se estiver em ambiente Java, camelCase, em Python, snake_case.

## 4.5 Padronize a entrada de suas APIs

Também é interessante padronizar o mecanismo de entrada de suas APIs. É importante verificar em quais casos você utilizará **Form Param, Form URL Encoded, RAW, Binary, etc**. Mantenha novamente consistência. O suporte a serialização pode tornar interessante a transferência de mensagens em formato JSON. Em várias linguagens existem diversos mecanismos e bibliotecas para serializar e desserializar o JSON ou XML caso necessário.

## 4.6 Sempre use HTTPS

**As pessoas podem acessar suas APIs de diversos locais** (shoppings, em casa, aeroportos, bancos, restaurantes, etc). **Devemos tomar cuidado**, pois nunca se sabe se não há ninguém interceptando as mensagens. Não deixe as pessoas acessaram sua API sem o uso de HTTPS.

## 4.7 Para alguns tipos de requisição, utilize Query Params.

Você já deve ter visto algo como o seguinte:

- GET /clientes?ativo=true

São os chamados **Query Params**. É interessante utilizar este tipo de parâmetro em situações de busca, filtro, ordenação, status, paginação, etc.

## 4.8 Cache e Autenticação

Para dados que não mudam frequentemente e não são sensíveis a erro, é interessante a utilização de caches para otimizar a performance de sua API.

Mecanismos de autenticação são comuns na maior parte das APIs hoje em dia. Temos diversas formas de realizar autenticação, como por exemplo:

- Sem autorização.
- Bearer Token.
- Basic Auth.
- Digest Auth.
- OAuth 1.0.
- OAuth 2.0
- Hawk Authentication.
- AWS Signature.
- Dentre outros mecanismos.

É importante antes de tudo verificar o nível de autenticação que você deseja em sua API. Para acessar serviços do governo Brasileiro (tais como dados fiscais), por exemplo, é necessário utilizar certificados digitais. Já em casos de Login de usuário em sistemas que não precisam de mecanismos elevados de segurança talvez seja mais interessante utilizar JWT. Note que dependendo do tipo de API, a legislação pode influenciar na forma de autenticação que você irá escolher.

## 4.9 Faça o uso de Logs

**Logs em excesso podem degradar a performance** de um sistema. Porem, **quando bem usados, criam mecanismos que auxiliam muito no processo de debug**. Dentre algumas práticas:

- Tenha uma estrutura consistente de Logs.
- Use níveis de severidade de um Log (Debug, Info, Warn, Error, etc).
- Forneça uma boa descrição para o Log, indicando todo o contexto do problema.
- Demonstre dados de contexto do erro.
- Utilize uma estrutura de data e hora.
- Realize log de exceções e alertas.
- Tenha um mecanismo centralizado que lhe permita acessar seus Logs de forma fácil e rápida.
- Em logs, qualidade é mais importante que quantidade.
- Verifique algumas ferramentas para lhe auxiliar no processo de Log. Ex: Log4j, Log4net, etc.

## 4.10 Tenha métricas sobre suas APIs

É importante ter dados que permitam verificar se sua API está sendo muito utilizada, ou se algum erro está ocorrendo com ela. Dois tipos interessantes de Métricas seriam a Quantidade de Requisições realizadas, e a Taxa Percentual do Status HTTP (Ex: 1xx: 0#, 2xx: 99%, 3##: 0%, 4xx: 1%, 5xx: 0%.

Note que caso esteja utilizando plataformas como AWS, Google Cloud ou Microsoft Azure, você terá mecanismos que facilitam esse controle.

As métricas lhe permitem ver se há erros, se há excesso de requisições, a quantidade de requisições, as requisições mais chamadas, etc. Isso lhe permite aprimorar o sistema e corrigir eventuais problemas.

## 4.11 Forneça mensagens de retorno descritivas

Vamos supor que você esteja tentando realizar a seguinte requisição:

- POST /clientes

Porem lhe é retornado o seguinte:

**{
“codigo”: 1,
“mensagem”: “Algo deu errado”,
“description”: “Aconteceram alguns erros ao adicionar este cliente”
}**

A interface deve fazer validações para auxiliar o usuário e tornar tudo mais intuitivo e dinâmico, porem é importante que sua API tenha validações a fim de promover consistência em seus dados. Um retorno mais interessante seria o seguinte:

**{
“codigo”: 1,
“mensagem”: “Erro de validação”,
“erros”: [{
“codigo”: 100,
“campo”: “email”,
“mensagem”: “E-mail deve ter no máximo 120 caracteres”
},
{
“codigo”: 101,
“campo”: “nome”,
“mensagem”: “Nome deve ter no máximo 100 caracteres”
},
{
“codigo”: 102,
“campo”: “senha”,
“mensagem”: “Senha não pode ser vazia”
}
]
}**

Assim, você garante que independente de quem estiver realizando a requisição (sistema, site, aplicativo, terceiros), as informações serão consistentes.

## 4.12 Divida sua API em camadas se necessário

Ao estruturar uma API, é interessante dividi-la em camadas (tudo depende da necessidade, aqui demonstraremos um exemplo de divisão em camadas). Assim, cada camada terá sua responsabilidade específica. Um modelo interessante a se seguir, é o seguinte:

- **Camada de persistência de dados**: Lida com o banco de dados de nossa aplicação.
- **Camada de serviço/negócios:** Contem as lógicas de negócio de nossa aplicação.
- **Camada de recurso:** Realiza a exposição dos recursos.

Vale ressaltar que **adição de camadas inclui benefícios (desacoplamento, coesão, etc), porem também impacta em desempenho**, então é necessário analisar os tradeoffs. A figura abaixo demonstra um exemplo em Java utilizando Jersey.

![img](https://miro.medium.com/max/60/0*N9aKlTljnA4Q8ETy.png?q=20)

![img](https://miro.medium.com/max/532/0*N9aKlTljnA4Q8ETy.png)

## 4.13 Faça paginação em quantidade de dados elevadas

No caso de uma lista com uma grande quantidade de dados, uma boa prática é a realização de paginação. Retornar 100.000 clientes em um único JSON acaba não sendo uma solução muito interessante. Na paginação, podemos passar alguns dados a nossa API:

- Quantidade de registros a ser retornada.
- Página que desejamos.
- Ordenação.

No retorno, é interessante mostrar a página atual e a quantidade total de páginas totais se possível. Exemplo de requisição:

- GET /clientes?page=1&pageSize=10&sort=nome

Também é interessante retornar no corpo de resposta a página anterior e a próxima página (se houver em ambos os casos) e outros dados úteis. Exemplo de resposta:

**{
“dados” : [
{ dado1 },
{ dado2 },
…
],
“paginacao”: {
“paginaAtual”: 2,
“quantidadeDeItens”: 10,
“anterior”: “/clientes?pagina=1&pageSize=10”,
“proximo”: “/clientes?pagina=3&pageSize=10”
}**

**}**

# 5. Linguagens de programação e plataformas para publicar as APIs

Agora que já sabemos as melhores práticas para o desenvolvimento das APIs, é chegada a hora de escolher uma linguagem de programação para desenvolver as APIs e um ambiente para publica-las.

## 5.1 — Entendendo Contexto e requisitos do sistema

É necessário entendermos que tipo de problema estamos tentando resolver, quais os requisitos funcionais e não funcionais que devemos satisfazer, compreender o domínio e contexto do problema em que iremos atuar, o que o usuário e ou cliente espera do sistema e como o mesmo agregará valor. Devemos entender aspectos de qualidade que o sistema deve fornecer, como: disponibilidade, segurança, desempenho, usabilidade, portabilidade, etc. Com isso, poderemos nos situar melhor na escolha de uma tecnologia.

## 5.2 — Critérios de escolha da linguagem

Ao escolher a linguagem, é interessante analisar uma série de fatores:

- Documentação fornecida.
- Força da comunidade.
- Conhecimento prévio.
- Bibliotecas e componentes fornecidos.
- Adoção pelo mercado.
- Arquitetura da linguagem (Java, JavaScript, C#, Erlang, Elixir, C++, Rust, Go, Python, PHP, Groovy, Scala, Perl, etc) e do ambiente em que ela executa.
- Compatibilidade entre o que a linguagem fornece e o seu sistema tenta resolver.
- Estabilidade da linguagem.
- Cultura da organização.
- Facilidades que cada linguagem fornece.
- Desempenho da linguagem.
- Produtividade.
- Bugs conhecidos na linguagem.
- Facilidade de desenvolvimento.
- Ambiente necessário para a execução da linguagem escolhida.
- Dentre outros critérios.

Com isso, teremos uma boa noção de cada linguagem e idealmente uma boa quantidade de alternativas. Dada as alternativas, deve ser escolhida a linguagem que melhor resolve o problema dados os critérios acima. Sempre é importante analisar o custo/benefício que a linguagem fornecerá em seu projeto.

## 5.3 — Exemplos de APIs em diferentes linguagens de programação

Abaixo há uma série de linguagens que podem ser utilizadas para desenvolver APIs, inclusive, com exemplos em código de como ficam as APIs:

- Java — Spring.

<iframe src="https://medium.com/media/34f4be87c4e55ca049482dffb846658e" allowfullscreen="" frameborder="0" height="1488" width="680" title="JavaSpringBoot.java" class="ef es eo ex w" scrolling="auto" style="box-sizing: inherit; width: 680px; position: absolute; left: 0px; top: 0px; height: 1487.99px;"></iframe>

- Java — Jersey

<iframe src="https://medium.com/media/9a1093a299c49ca7db72f02c0c77ed94" allowfullscreen="" frameborder="0" height="1337" width="680" title="JavaJersey.java" class="ef es eo ex w" scrolling="auto" style="box-sizing: inherit; width: 680px; position: absolute; left: 0px; top: 0px; height: 1337px;"></iframe>

- C# — .NET Core.

<iframe src="https://medium.com/media/73861460440174702a86a8c5305f92ab" allowfullscreen="" frameborder="0" height="831" width="680" title="DotNetCore.cs" class="ef es eo ex w" scrolling="auto" style="box-sizing: inherit; width: 680px; position: absolute; left: 0px; top: 0px; height: 830.99px;"></iframe>

- JavaScript — Node.js.

<iframe src="https://medium.com/media/d8b81cd9913c05bfdfb2075ac84a3245" allowfullscreen="" frameborder="0" height="1132" width="680" title="Node.js" class="ef es eo ex w" scrolling="auto" style="box-sizing: inherit; width: 680px; position: absolute; left: 0px; top: 0px; height: 1132px;"></iframe>

- Python — Flask.

<iframe src="https://medium.com/media/17c1b8b11b6a6da23e310e77871149c3" allowfullscreen="" frameborder="0" height="1311" width="680" title="Flask.py" class="ef es eo ex w" scrolling="auto" style="box-sizing: inherit; width: 680px; position: absolute; left: 0px; top: 0px; height: 1310.99px;"></iframe>

- Elixir — Maru.

<iframe src="https://medium.com/media/d145ac32ac8a71a43b902bf524276381" allowfullscreen="" frameborder="0" height="458" width="680" title="Elixir.ex" class="ef es eo ex w" scrolling="auto" style="box-sizing: inherit; width: 680px; position: absolute; left: 0px; top: 0px; height: 457.986px;"></iframe>

- PHP — Laravel.

<iframe src="https://medium.com/media/6d097f075cc3df30e110561ae691175f" allowfullscreen="" frameborder="0" height="1464" width="680" title="PhpLaravel.php" class="ef es eo ex w" scrolling="auto" style="box-sizing: inherit; width: 680px; position: absolute; left: 0px; top: 0px; height: 1463.99px;"></iframe>

- Rust — Rocket.

<iframe src="https://medium.com/media/58a083fa66c441969079988a1abf7842" allowfullscreen="" frameborder="0" height="590" width="680" title="Rust.rs" class="ef es eo ex w" scrolling="auto" style="box-sizing: inherit; width: 680px; position: absolute; left: 0px; top: 0px; height: 590px;"></iframe>

- Go

<iframe src="https://medium.com/media/40b388228cc355170291b51177a9bc90" allowfullscreen="" frameborder="0" height="1641" width="680" title="Go.go" class="ef es eo ex w" scrolling="auto" style="box-sizing: inherit; width: 680px; position: absolute; left: 0px; top: 0px; height: 1640.99px;"></iframe>

- Dart

<iframe src="https://medium.com/media/f71f897a23088eb081628f5ffc755bea" allowfullscreen="" frameborder="0" height="2216" width="680" title="Dart.dart" class="ef es eo ex w" scrolling="auto" style="box-sizing: inherit; width: 680px; position: absolute; left: 0px; top: 0px; height: 2215.99px;"></iframe>

## 5.4 —Escolhendo uma “plataforma” para a execução da API

Antes de realizar a hospedagem da API, precisamos entender alguns conceitos:

- **IAAS — Infrastructure as a Service:** Empresa contrata uma capacidade de hardware, memória, armazenamento, processamento, etc. Te fornece um maior nível de flexibilidade e controle do gerenciamento sobre seus recursos, sendo geralmente o que os desenvolvedores mais comumente estão acostumados.
- **PAAS — Platform as a service**: Empresa contrata um ambiente completo de desenvolvimento onde se cria, modifica e otimiza software. Modelo focado em se preocupar mais com a programação do que com o gerenciamento da infraestrutura.
- **SAAS — Software as a Service**: É basicamente o software como um serviço, como Facebook, Twitter, Skype, etc. Nesta categoria, se oferece um produto.
- Uma boa documentação a ser acessada é sobre os [tipos de computação em Nuvem é a da Amazon Web Services](https://aws.amazon.com/pt/types-of-cloud-computing/), que descreve alguns outros detalhes como implantação tanto em nuvem, híbrida e local.

Abordado estes conceitos, iremos verificar alguns provedores de computação em nuvem:

- Amazon Web Services.
- Azure.
- Google Cloud Platform.
- IBM Cloud.
- Oracle Cloud.
- Alibaba Cloud.
- Dentre diversas outras.

Segue abaixo uma pesquisa realizada pela ZDNET em 2019:

![img](https://miro.medium.com/max/60/0*6adlYvG8S7bzzHX3.png?q=20)

![img](https://miro.medium.com/max/630/0*6adlYvG8S7bzzHX3.png)

Ao utilizar a ferramenta do Google Trends, podemos visualizar os seguintes dados baseados nos últimos 12 meses (pesquisa feita dia 03/11/2019):

![img](https://miro.medium.com/max/60/1*2Wi2_8aRWz3zQFiReXtk0A.png?q=20)

![img](https://miro.medium.com/max/630/1*2Wi2_8aRWz3zQFiReXtk0A.png)

Também podemos visualizar estes dados por regiões no brasil.

![img](https://miro.medium.com/max/60/1*zABUFXDQ8qJGwe9YEfMnFA.png?q=20)

![img](https://miro.medium.com/max/630/1*zABUFXDQ8qJGwe9YEfMnFA.png)

Devemos antes de escolher uma plataforma fazer um estudo prévio, contendo alguns dos seguintes aspectos :

- Recursos que cada uma das soluções oferece.
- Serviços que utilizaremos.
- Custo para a execução.
- Quantidade de documentação presente em cada solução.
- Nível de suporte e auxilio que a plataforma fornece.
- Quantidade de conteúdo disponível.
- Comunidade que utiliza a plataforma.
- Dentre outros.

Geralmente, é fornecido um período de teste de 12 meses para que você possa se acostumar e estudar a plataforma. Note que existem limitações neste período de teste, que caso excedidas, podem gerar custos. Feito um estudo melhor de cada solução, podemos nos perguntar:

- Utilizarei de um SGBD relacional (MySQL, Postgree, SQL Server, etc) ou uma solução NoSQL (MongoDB, DynamoDB, etc) ?
- Utilizarei algum mecanismo de armazenamento em memória como o Redis ou Memcached ?
- Utilizarei algum produto de API Gateway fornecido pelas soluções (API Gateway AWS, API Gee da Google Cloud, etc) ?
- A plataforma suporta a hospedagem para a linguagem de programação e plataformas que estou utilizando ?
- Utilizarei uma arquitetura monolítica ou de microserviços? Devo utilizar computação serverless?
- Onde armazenarei meus “objetos” (documentos, arquivos, imagens, etc) ? Através da Amazon S3, Google Cloud Storage, Azure Blob ou outra solução?
- Qual o suporte a CDN (Content delivery Network) em cada uma das soluções? Em quais produtos está integrado ?
- Devo escalar verticalmente ou horizontalmente ? Qual das suas opções é mais viável para minha situação atual ?
- Quais os parâmetros de escalabilidade utilizarei para incrementar ou decrementar instancias ?
- A solução contem um mecanismo de DNS (Route 53, etc) ?
- Qual o custo mensal de todos os recursos que necessito ?
- Dentre outras questões.

## 5.5— Verificando custos

Custos são extremamente relativos. Variam de acordo com a necessidade, e são influenciados por diversos parâmetros.

- AWS

[Definição de preço](https://aws.amazon.com/pt/pricing/?nc2=h_ql_pr_calc)

[Limite gratuito](https://aws.amazon.com/pt/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc)

[Calculadora de preços](https://calculator.s3.amazonaws.com/index.html?nc2=h_ql_pr_calc_smc)

[Otimização de custo](https://aws.amazon.com/pt/pricing/cost-optimization/?nc2=h_ql_pr_opt)

[Calculadora de preço para AWS Lambda — Serverless computing](https://aws.amazon.com/pt/lambda/pricing/)

- Google Cloud Storage

[Definição de preço](https://cloud.google.com/storage/pricing-summary/)

[Limite gratuito](https://cloud.google.com/free/)

[Lista de preços por produto](https://cloud.google.com/pricing/list)

[Calculadora de preços](https://cloud.google.com/products/calculator/)

[Calculadora de preço para Google Cloud Function — Servlerless computing](https://cloud.google.com/functions/pricing-summary/?hl=pt-br)

- Azure

[Definição de preço](https://azure.microsoft.com/en-us/pricing/)

[Limite gratuito](https://azure.microsoft.com/pt-br/free/)

[Calculadora de preços](https://azure.microsoft.com/en-us/pricing/calculator/?&ef_id=Cj0KCQjw9fntBRCGARIsAGjFq5H3fKMC8q2PUn2-KJum1J_XA-Rr59WwmGVG3Ae9SqgO8R8Td0QUPBYaAg6cEALw_wcB:G:s&OCID=AID2000058_SEM_566EkZFH&MarinID=566EkZFH_380028600406_azure price_e_c__76392000876_kwd-296465858779&lnkd=Google_Azure_Brand&dclid=CjgKEAjw9fntBRC_itO7wICp2HISJADeKf38Xb4cFTocHkV0cpe1jlSe6S-4peiuVaYHP98F6fGm5PD_BwE)

[Calculadora de preço para Azure Function — Serverless computing](https://azure.microsoft.com/pt-br/pricing/details/functions/)

# 6. Agradecimentos

Espero que este artigo tenha contribuído de alguma forma sobre a arquitetura das APIs RESTful. O passo após a publicação da API é o monitoramento. Tentei resumir alguns pontos importantes e traze-los para discussão neste artigo. Espero que tenham um bom proveito.

# Referências:

Capitulo 5 da Tese de Doutorado de Roy Fielding. Disponível em https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm.

Artigos de Marcos Mendes. Disponível em https://marco-mendes.com/arquitetura/.

Melhores práticas para o design de APIs RESTFUL pragmáticas. Disponível em https://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api.

Imagens disponibilizadas pelo Pluralsight. Disponível em https://www.pluralsight.com/blog/tutorials/representational-state-transfer-tips.

Http basics. Disponível em https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/HTTP_Basics.html.

API da Marvel. Disponível em [https://developer.marvel.com/docs.](https://developer.marvel.com/docs)

Developer Mozilla. Disponível em https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status.

Tabela de métodos. Disponível em https://medium.com/@kumaraksi/using-http-methods-for-restful-services-e6671cf70d4d.

Notas sobre idempotencia. Disponível em https://stackoverflow.com/questions/4088350/is-rest-delete-really-idempotent

RFC 2616. Disponível em https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html.

RFC 7231. Disponível em https://tools.ietf.org/html/rfc7231#section-4.2.2.

Martin Fowler — Modelo de maturidade de Richardson. Disponível em https://martinfowler.com/articles/richardsonMaturityModel.html.

Melhores práticas para Logs. Disponível em https://www.loomsystems.com/blog/single-post/2017/01/26/9-logging-best-practices-based-on-hands-on-experience.

Rest Api Design. Disponível em https://www.codepedia.org/ama/tutorial-rest-api-design-and-implementation-in-java-with-jersey-and-spring/.

RestFul web service with Jersey. Disponível em https://o7planning.org/en/11207/simple-crud-example-with-java-restful-web-service.

RestFul webservice with Python. Disponível em https://kite.com/blog/python/flask-restful-api-tutorial/.

RestFul webservice with Elixir. Disponível em https://dev.to/plutov/building-rest-server-with-elixir-4pd.

RestFul webservice with Php Laravel. Disponível em https://www.toptal.com/laravel/restful-laravel-api-tutorial.

RestFul webservice with Rust. Disponível em [https://www.toptal.com/laravel/restful-laravel-api-tutorial.](https://medium.com/sean3z/building-a-restful-crud-api-with-rust-1867308352d8)

RestFul webservicw with Go. Disponível em https://medium.com/@rafaelacioly/construindo-uma-api-restful-com-go-d6007e4faff6.

RestFul webservicw with Dart. Disponível em [https://medium.com/@rafaelacioly/construindo-uma-api-restful-com-go-d6007e4faff6.](https://itnext.io/building-restful-web-apis-with-dart-aqueduct-and-postgresql-3cc9b931f777)

Top cloud providers 2019. Disponível em https://www.zdnet.com/article/top-cloud-providers-2019-aws-microsoft-azure-google-cloud-ibm-makes-hybrid-move-salesforce-dominates-saas/.