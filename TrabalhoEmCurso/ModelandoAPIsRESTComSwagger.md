# Modelando APIs REST com Swagger

Alexandre Aquiles and Rodrigo Ferreira

6 anos atrás

![img](data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjMzNiIgd2lkdGg9IjEwMDAiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgdmVyc2lvbj0iMS4xIi8+)![swagger-logo](https://i1.wp.com/blog.caelum.com.br/wp-content/uploads/2035/02/swagger-logo.png?fit=1000%2C336&ssl=1)

Atualmente é bem comum que empresas utilizem *APIs REST* para a integração de aplicações, seja para consumir serviços de terceiros ou prover novos serviços.

Ao consumir uma API existente, precisamos conhecer as funcionalidades disponíveis e detalhes de como invocá-las: recursos, URIs, métodos, Content-Types e outras informações.

Ao prover uma nova API REST, além da implementação, há outras duas preocupações comuns: como **modelar** e **documentar** a API?

## Ferramentas para modelagem e documentação de APIs REST

Em um Web Service do estilo *SOAP* temos o *WSDL*, que funciona como uma documentação (para máquinas) do serviço, facilitando a geração automatizada dos clientes que vão consumi-lo. Além disso, podemos modelar nosso serviço escrevendo o WSDL, em uma abordagem conhecida como *Contract-First*. Não é nada legível nem fácil de escrever, mas funciona. Só que no mundo dos Web Services REST não temos o WSDL. E agora?

Algumas ferramentas para nos auxiliar nessa questão foram criadas, e dentre elas temos: WSDL 2.0, WADL, API Blueprint, RAML e Swagger.

Neste post vamos abordar o **Swagger**, que é uma das principais ferramentas utilizadas para modelagem, documentação e geração de código para APIs do estilo REST.

## Mas o que exatamente é o Swagger?

O Swagger é um projeto composto por algumas ferramentas que auxiliam o desenvolvedor de APIs REST em algumas tarefas como:

- Modelagem da API
- Geração de documentação (legível) da API
- Geração de códigos do Cliente e do Servidor, com suporte a várias linguagens de programação

Para isso, o Swagger especifica a **OpenAPI**, uma linguagem para descrição de contratos de APIs REST. A [OpenAPI](https://github.com/OAI/OpenAPI-Specification) define um formato JSON com campos padronizados (através de um [JSON Schema](http://json-schema.org/)) para que você descreva recursos, modelo de dados, URIs, Content-Types, métodos HTTP aceitos e códigos de resposta. Também pode ser utilizado o formato YAML, que é um pouco mais legível e será usado nesse post.

Além da OpenAPI, o Swagger provê um ecossistema de ferramentas. As principais são:

- [Swagger Editor](http://swagger.io/swagger-editor/) – para a criação do contrato
- [Swagger UI](http://swagger.io/swagger-ui/) – para a publicação da documentação
- [Swagger Codegen](http://swagger.io/swagger-codegen/) – para geração de “esqueletos” de servidores em mais de 10 tecnologias e de clientes em mais de 25 tecnologias diferentes

Nesse post, vamos focar na parte de modelagem de uma nova API. Futuramente teremos outro post focando na documentação de uma API já existente.

## Modelando a API da Payfast

Para modelar nossa nova API, utilizaremos o Swagger Editor. Você pode [instalá-lo localmente](https://github.com/swagger-api/swagger-editor#running-locally), executando uma aplicação NodeJS, ou utilizar a versão online em [editor.swagger.io](http://editor.swagger.io/).

Vamos modelar a API da Payfast, uma aplicação de pagamentos bem simples que é estudada no curso [SOA na prática](https://www.caelum.com.br/curso-java-ee-soa-web-services-mensageria/).

Pra começar, devemos definir algumas informações iniciais, como a versão do Swagger que estamos usando:

```
swagger: '2.0'
```

O título, descrição e versão da API devem ser definidos:

```
info:
  title: Payfast API
  description: Pagamentos rápidos
  version: 1.0.0
```

Em `host`, inserimos o endereço do servidor da API, em `basePath` colocamos o contexto da aplicação e em `schemes` informamos se a aplicação aceita HTTP e/ou HTTPS.

```
host: localhost:8080
basePath: /fj36-payfast/v1
schemes:
  - http
  - https
```

## Defininindo o modelo de dados

De alguma forma, precisamos definir quais dados são recebidos e retornados pela API.

Na nossa API, recebemos dados de uma *Transação*, que tem um código, titular, data e valor. A partir disso, geramos um *Pagamento* com id, status e valor.

![img](data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjEwMyIgd2lkdGg9IjI5NSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB2ZXJzaW9uPSIxLjEiLz4=)







Em um WSDL, esse modelo de dados é definido através de um XML Schema (XSD). No caso do Swagger, o modelo de dados fica em um [JSON Schema](http://json-schema.org/) na seção `definitions` do contrato.

De acordo com o JSON Schema, em `type` podemos usar tipos primitivos de dados para números inteiros (`integer`), números decimais (`number`), textos (`string`) e booleanos (`boolean`). Esses tipos primitivos podem ser modificados com a propriedade `format`. Para o tipo `integer` temos os formatos `int32` (32 bits) e `int64` (64 bits, ou long). Para o `number`, temos os formatos `float` e `double`. Não há um tipo específico para datas, então temos que utilizar uma `string` com o formato `date` (só data) ou `date-time` (data e hora).

Além dos tipos primitivos, podemos definir objetos com um `type` igual a `object`. Esses objetos são compostos por várias outras propriedades, que ficam em `properties`.

No nosso caso, o modelo de dados com os objetos `Transacao` e `Pagamento` ficaria algo como:

```
definitions:
  Transacao:
    type: object
    properties:
      codigo:
        type: string
      titular:
        type: string
      data:
        type: string
        format: date
      valor:
        type: number
        format: double
  Pagamento:
    type: object
    properties:
      id:
        type: integer
        format: int32
      status:
        type: string
      valor:
        type: number
        format: double
```

## Defininindo os recursos da API

Com o modelo de dados pronto, precisamos modelar os recursos da nossa API e as respectivas URIs. No Payfast, teremos o recurso `Pagamento` acessível pela URI `/pagamentos`.

Um POST em `/pagamentos` cria um novo pagamento. Se o pagamento criado tiver o id 1, por exemplo, as informações estariam acessíveis na URI `/pagamentos/1`.

Podemos fazer duas coisas com o nosso pagamento: para confirmá-lo, devemos enviar um PUT para `/pagamentos/1`; para cancelá-lo, enviamos um DELETE.

![img](data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjIyOCIgd2lkdGg9IjU0MyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB2ZXJzaW9uPSIxLjEiLz4=)







No Swagger, as URIs devem ser descritas na seção `paths`:

```
paths:
  /pagamentos:
    post:
      summary: Cria novo pagamento

  /pagamentos/{id}:
    put:
      summary: Confirma um pagamento
    delete:
      summary: Cancela um pagamento
```

## Definindo os parâmetros de request

Para a URI `/pagamentos`, que recebe um POST, é enviada uma transação no corpo da requisição, que deve estar no formato JSON. É feita uma referência ao modelo `Transacao` definido anteriormente.

```
paths:
  /pagamentos:
    post:
      summary: Cria novo pagamento
      consumes:
        - application/json
      parameters:
        - in: body
          name: transacao
          required: true
          schema:
            $ref: '#/definitions/Transacao'
```

Já para a URI `/pagamentos/{id}`, é definido um *path parameter* com o id do pagamento. Esse parâmetro pode ser descrito na seção `parameters`, logo acima da seção `paths`, e depois referenciado nos métodos.

```
parameters:
  pagamento-id:
    name: id
    in: path
    description: id do pagamento
    type: integer
    format: int32
    required: true
paths:
  /pagamentos:
    #código omitido... 

  /pagamentos/{id}:
    put:
      summary: Confirma um pagamento
      parameters:
        - $ref: '#/parameters/pagamento-id'
    delete:
      summary: Cancela um pagamento
      parameters:
        - $ref: '#/parameters/pagamento-id'
```

## Definindo os tipos de response

Definidos os parâmetros de *request*, precisamos modelar o *response*.

Depois da criação do pagamento, deve ser retornado um response com o status `201` (Created) juntamente com a URI do novo pagamento no *header* `Location` e uma representação em JSON no corpo da resposta.

```
paths:
  /pagamentos:
    post:
      summary: Cria novo pagamento
      consumes:
        - application/json
      produces:
        - application/json
      #código omitido...
      responses:
        '201':
          description: Novo pagamento criado
          schema:
            $ref: '#/definitions/Pagamento'
          headers:
            Location:
              description: uri do novo pagamento
              type: string
```

Após a confirmação de um pagamento, é simplesmente retornado o status `200` (OK). O mesmo retorno acontece após um cancelamento.

```
/pagamentos/{id}:
    put:
      summary: Confirma um pagamento
      parameters:
        - $ref: '#/parameters/pagamento-id'
      responses:
        '200':
          description: 'Pagamento confirmado'
    delete:
      summary: Cancela um pagamento
      parameters:
        - $ref: '#/parameters/pagamento-id'
      responses:
        '200':
          description: 'Pagamento cancelado'
```

O contrato final do exemplo utilizado pode ser aberto no Swagger Editor em: [bit.ly/swagger-editor-payfast-api](http://bit.ly/swagger-editor-payfast-api)

Perceba que no menu superior temos a opção *Generate Server* para gerar um esqueleto do servidor em Java (JAX-RS e Spring-MVC), PHP (Slim e Silex), Python (Flask), entre outras tecnologias. Há também a opção *Generate Client*, que gera clientes nessas tecnologias e em diversas outras.

## Concluindo

A abordagem utilizada nesse post foi a conhecida como *Contract-First* ou *API-First Development*.

Modelamos a API pensando nos dados, nos recursos, URIs, métodos, parâmetros e respostas. Começamos a definição do serviço criando primeiro a API de comunicação, para só posteriormente pensar na implementação.

Esta abordagem gera um desacoplamento entre implementação e interface de uso, além de permitir que tando o lado cliente quanto o lado servidor possam iniciar seu desenvolvimento assim que a API estiver definida, mesmo sem uma implementação finalizada.

Uma outra abordagem (talvez mais comum) é começar pela implementação para só depois pensar na documentação e talvez realizar ajustes de modelagem. Essa abordagem é conhecida como *Contract-Last* e o uso dela com Swagger será abordado em outro post.

E você? Já usou o Swagger em algum projeto para modelar uma nova API, no estilo Contract-First? Conte-nos como foi a experiência!