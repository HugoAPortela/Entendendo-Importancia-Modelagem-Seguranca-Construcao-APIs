# Segurança em APIs REST

![Segurança de API REST](https://img.mandic.com.br/blog/2013/06/dilbert_04072012_seguranca.jpg)

Uma das dúvidas mais comuns na implementação de [APIs](https://en.wikipedia.org/wiki/Application_programming_interface) [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) é sobre **como garantir a segurança dos serviços**. Como muitas coisas em software, há várias opções, e vamos dar uma visão geral sobre as possibilidades, com uma boa dose de opinião.

## De quanta segurança você precisa?

O esforço na implementação de segurança e seu custo deve avaliar algumas questões principais. Claro que o ideal seria termos somente sistemas absolutamente seguros, porém isto pode trazer custos pesados e a decisão vai sempre levar em conta o que é “*bom o suficiente*”.

### Sua API é pública ou privada?

Parte das ações relativas a segurança depende de infraestrutura e parte depende de desenvolvimento. Sem dúvidas uma **API privada** pode ser muito mais blindada pela infraestrutura e talvez as preocupações dos desenvolvedores fiquem bem suaves. Já numa **API pública** o grau de exposição é bem maior e o leque de atacantes é desconhecido, exigindo do desenvolvimento uma série de verificações para garantir acessos legítimos e autorizados.

### Quão sensíveis são os dados?

Ninguém quer permitir acessos indevidos às suas **APIs**, mas é claro que vazamentos de dados sobre os times e escalações do jogador no Cartola são menos preocupantes do que vazamentos num [ERP](https://en.wikipedia.org/wiki/Enterprise_resource_planning) ou [CRM](https://en.wikipedia.org/wiki/Customer_relationship_management). Quanto mais interessantes os dados para uma pessoal mal-intencionada, mais críticos devem ser os bloqueios no acesso.

Uma observação importante é que é fundamental acompanhar as **APIs de produtos** eventualmente construídos fora da empresa. Um amigo de uma importante empresa de tecnologia de SP me contou que seu RH uma vez contratou um sistema de folha de pagamento que disponibilizava abertamente uma URL que listava TODOS os salários da empresa. Esta é uma falha catastrófica mesmo que os dados não saiam de dentro da empresa, e mostra a importância do processo de segurança permear tanto os desenvolvimentos internos como os terceirizados.

### Uma brecha no seu sistema abre acesso para outros sistemas internos?

Hoje em dia o desenvolvimento de **componentes com APIs** é cada vez mais frequente e um sistema normalmente se integra com um ou mais sistemas da mesma empresa. Se suas **APIs** abrem possibilidades de interação em outros sistemas da empresa, os cuidados devem ser redobrados.

## Mecanismos de segurança comuns

O **controle da segurança** muitas vezes se utiliza de mais de um mecanismo e a abordagem pode ser bem sofisticada. Falaremos aqui de exemplos bastante encontrados.

### Restrição de acesso pela infraestrutura de rede

Em **APIs internas**, às vezes o **controle da segurança** fica totalmente implementado pela infraestrutura. Restrições de acesso por IP implementados em roteadores, firewalls e balanceadores de carga. Restrição também de protocolos de comunicação permitidos e portas, logging detalhado dos acessos realizados.

Isto também é possível em ambientes de nuvem como a [Amazon Web Services](https://www.mandic.com.br/aws/), através de grupos de segurança, firewalls internos nas instâncias, controle no [Elastic Load Balancer](https://www.mandic.com.br/aws/amazon-cloud-recursos/#AWS-Elastic-Load-Balancer), [VPCs](https://www.mandic.com.br/aws/amazon-cloud-recursos/#Amazon-Virtual-Private-Cloud), entre outras formas.

### Comunicações HTTPS

O [HTTPS](https://en.wikipedia.org/wiki/HTTP_Secure) é um protocolo para comunicações seguras que vem sendo amplamente utilizado na internet há muitos anos. Ele provê autenticação entre usuários finais e servidores, e também na comunicação entre servidores.

Ele já protege contra ataques [man-in-the-middle](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) e provê criptografia bilateral entre cliente e servidor, protegendo contra [Eavesdropping](https://en.wikipedia.org/wiki/Eavesdropping) e [Tampering](https://en.wikipedia.org/wiki/Tamper-evident#Tampering). Servidores que se comuniquem via HTTPS possuem chance muito menor de brechas de segurança. Sendo usado em conjunto com a restrição de acesso na rede, já é uma solução bem **segura para APIs privadas** na maioria dos casos.

### Autenticação/Autorização HTTP basic

A [autenticação HTTP basic](https://en.wikipedia.org/wiki/Basic_access_authentication) é uma forma bem simples de um cliente informar suas credenciais de acesso ao fazer uma requisição HTTP. Ela é a técnica mais simples de exigir controle de acesso a recursos web, pois não requer [cookies](https://en.wikipedia.org/wiki/HTTP_cookie), [identificadores de sessão](https://en.wikipedia.org/wiki/Session_identifier) ou páginas de login. São usados somente cabeçalhos HTTP estáticos, que não exigem handshake antes do início da comunicação.

Na autenticação HTTP Basic, o usuário e senha do cliente são enviados ao servidor codificados em [Base64](https://en.wikipedia.org/wiki/Base64). Esta forma de autenticação provê algum controle de acesso, mas é vulnerável a interceptações na rede, que permitiriam que o atacante obtivesse o usuário e senha e passasse a fazer requisições usando os dados obtidos. Porém, o uso de HTTPS para proteger o canal resolve este problema.

Em linhas gerais a comunicação funciona conforme abaixo.

![Autenticação/Autorização HTTP basic](https://img.mandic.com.br/blog/2013/06/http_basic.jpg)

### Autenticação/Autorização HTTP Digest

A autenticação [HTTP Digest](https://en.wikipedia.org/wiki/Digest_access_authentication) é outra forma de controle de acesso a recursos web, e é mais segura que a [HTTP Basic](https://en.wikipedia.org/wiki/Basic_access_authentication). Ela aplica um [hash criptográfico MD5](https://en.wikipedia.org/wiki/Cryptographic_hash) na senha antes de enviá-la pela rede, com uso de valores [nonce](https://en.wikipedia.org/wiki/Cryptographic_nonce) para prevenir contra [replay attacks](https://en.wikipedia.org/wiki/Replay_attack).

Os **cálculos MD5** usados na autenticação digest buscam ser unidirecionais, ou seja, deve ser difícil obter o valor de entrada somente a partir da saída. Porém, se a senha for muito simples não deve ser tão custoso o processo de quebra por [força-bruta](https://en.wikipedia.org/wiki/Brute-force_attack).
Em linhas gerais a comunicação funciona conforme abaixo.

[![Autenticação HTTP Digest](https://img.mandic.com.br/blog/2013/06/digest.jpg)](https://img.mandic.com.br/blog/2013/06/digest.jpg)

### Autenticação/Autorização através de Certificados

A autenticação/autorização através de certificados também do lado do cliente é um refinamento adicional de segurança sobre a comunicação HTTPS, que já pode ser feita com certificados só do lado do servidor. Esta forma de autenticação/autorização é bastante segura, porém o trabalho e custo de lidar com certificados dos 2 lados é razoável, sendo adequada só em cenários muito sensíveis de segurança.

### Token-based authorization

Esta é uma forma simples e segura de controlar autenticação/autorização de serviços entre servidores, embora não seja um padrão. Há alguns anos implementei algumas **APIs** usando esta forma. As etapas no geral são:

- 1 – Aplicação cliente autentica-se no servidor informando suas credenciais de acesso
- 2 – Aplicação servidora valida credenciais e em caso de sucesso guarda um token de autorização, vinculando-o ao IP de origem do cliente. Token podem ser válido por uma operação ou por um período (ex: 24 horas)
- 3 – Servidor envia mensagem de sucesso para o cliente e envia o token
- 4 – Cliente invoca serviços no servidor sempre enviando o token de autorização
- 5 – Servidor valida cada requisição checando se foi enviado um token válido. Se um token não foi enviado, já tiver expirado ou for inválido, o servidor retorna mensagem ao cliente exigindo autorização, da mesma forma que com HTTP Basic ou Digest.

### OAuth

O [OAuth](https://en.wikipedia.org/wiki/OAuth) é um padrão aberto para autorização. Ele provê um método para clientes acessarem recursos no servidor por parte do dono do recurso (como um outro cliente ou um usuário final). Ele também provê meios de usuários finais autorizarem acesso de terceiros a seus recursos em um servidor sem informar suas credenciais, normalmente através de redirects e confirmações por parte dos usuários.

O **OAuth** é comumente usado quando temos um aplicativo que precisa **manipular APIs** com dados de usuários finais e estes precisam autorizar o acesso. Exemplos típicos são aplicativos que conectam-se a conta do usuário em redes sociais.

Embora possa ser usado para autorizações entre servidores, isto não é muito comum. Embora seja seguro, o OAuth não tem adesão tão grande devido à complexidade na implementação. Exemplos abaixo para as versões 1.0 e 2.0

![OAuth fluxo de autenticação](https://img.mandic.com.br/blog/2013/06/oauth1.png)

![Aplication OAuth](https://img.mandic.com.br/blog/2013/06/oauth2.png)

## Conclusão

Há diversas formas de controlar a **segurança de APIs REST**, e neste post apresentamos formas comuns de fazê-lo. É possível criar protocolos customizados de autenticação/autorização, mas é altamente recomendável usar soluções já conhecidas.

Em posts futuros da série, mostraremos implementações prática destes mecanismos de segurança com Java e possivelmente outras linguagens.

Até a próxima!

 LINKEDIN

 FACEBOOK

 TWITTER

[ WHATSAPP](https://web.whatsapp.com/send?text=https%3A%2F%2Fblog.mandic.com.br%2Fartigos%2Fseguranca-em-apis-rest-parte-1%2F?utm_source=whatsapp&utm_medium=social&utm_campaign=Blog-Share)

Gostou do conteúdo? Tem alguma dúvida? Entre em contato com nossos **[Especialistas Mandic Cloud](https://www.mandic.com.br/atendimento/proposta-comercial/?origin=Artigos)**, ficamos felizes em ajudá-lo.

## Saiba mais

-  [REST é bom para todos os contextos na criação de APIs?](https://blog.mandic.com.br/artigos/rest-e-bom-para-todos-os-contextos-na-criacao-de-apis/)
-  [Uma abordagem de desenvolvimento API-First](https://blog.mandic.com.br/artigos/uma-abordagem-de-desenvolvimento-api-first/)
-  [Construindo APIs profissionais em Java](https://blog.mandic.com.br/artigos/material-da-palestra-de-apis-profissionais-em-java-no-tdc-2013/)
-  [Garanta a segurança contínua do seu ambiente em nuvem](https://www.mandic.com.br/solutions/seguranca-preventiva/)
-  [Cloud Compliance no Mandic Cloud Platform - MCP](https://platform.mandic.com.br/portfolio/cloud-compliance/)
-  [Webinar: Segurança em Cloud AWS e suas oportunidades para redução de riscos](https://labs.mandic.com.br/webinars/seguranca-cloud-aws-reducao-de-riscos-cadastro)