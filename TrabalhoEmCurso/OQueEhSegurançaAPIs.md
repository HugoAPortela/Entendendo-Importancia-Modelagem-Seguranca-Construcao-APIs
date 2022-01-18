# O que é segurança de APIs?

Segurança de APIs é a proteção à integridade das APIs que a sua empresa possui e usa. O que isso significa?

Provavelmente, você já ouviu falar de [Internet das Coisas (IoT)](https://www.redhat.com/pt-br/topics/internet-of-things), a tecnologia que proporciona aos objetos da vida cotidiana o poder da computação. Por exemplo, com a IoT, você pode conectar seu smartphone à sua geladeira para saber exatamente o que precisa comprar no supermercado depois do trabalho para aquele jantar combinado em cima da hora. Ou talvez você faça parte de uma equipe de [DevOps](https://www.redhat.com/pt-br/topics/devops) que usa microsserviços e containers para criar e implantar aplicações legadas e nativas em nuvem de maneira rápida e iterativa. [APIs](https://www.redhat.com/pt-br/topics/api) são um dos meios mais usados na comunicação entre microsserviços e containers, assim como entre sistemas e aplicações. À medida que integração e interconectividade ganham mais importância, o mesmo acontece com as APIs.

------

## Por que a segurança de APIs é importante?

Empresas usam [APIs](https://www.redhat.com/pt-br/topics/api/what-are-application-programming-interfaces) para conectar serviços e transferir dados. APIs com problemas, desprotegidas ou hackeadas são a causa das principais violações de dados. Elas podem expor publicamente dados médicos, financeiros e pessoais. Contudo, nem todos os dados têm a mesma importância e devem ser protegidos do mesmo modo. Sua abordagem de segurança de APIs a ser adotada dependerá do tipo de dados que são transferidos.  

Se a API usada por sua empresa se conectar a aplicações de terceiros, será necessário entender como essas aplicações direcionam as informações de volta para a Internet. Pensando no exemplo acima, talvez você não se importe que outra pessoa descubra o que há em sua geladeira. No entanto, se essa pessoa usar a mesma API para rastrear a sua localização, isso é um motivo para se preocupar. 

------

## O que é segurança de APIs web? Comparação entre a segurança de API REST e API SOAP

A segurança de APIs web tem como maior preocupação a transferência de dados por meio de APIs que estão conectadas à Internet. OAuth (Open Authorization) é o padrão open source para delegação de acesso. Esse padrão possibilita aos usuários conceder a terceiros acesso a recursos da web sem a necessidade de compartilhar senhas. OAuth é o padrão tecnológico que permite que você mostre para o mundo todo um [vídeo de cachorros engraçados](https://www.youtube.com/watch?v=XmsUMvoP7tg) nas suas redes sociais apenas com um clique no botão "Compartilhar".

A maioria das implementações de API é de [Transferência de Estado Representacional (REST) ou de Protocolo Simples de Acesso a Objetos (SOAP)](https://www.redhat.com/pt-br/topics/api/what-are-application-programming-interfaces).

As APIs REST usam HTTP e são compatíveis com [criptografia do protocolo de Transport Layer Security (TLS)](https://en.wikipedia.org/wiki/Transport_Layer_Security). O protocolo TLS é um padrão que mantém as conexões na Internet privadas e verifica se os dados transferidos entre dois sistemas (servidor-servidor ou servidor-cliente) estão criptografados e inalterados. Isso significa que um hacker que tenta expor as informações de cartão de crédito dos clientes por um site de compras não poderá ler nem modificar esses dados. Sabemos que um site é protegido pelo protocolo TLS quando a URL começa com o Protocolo de Transferência de Hipertexto Seguro (HTTPS). 

Além disso, as APIs REST usam o [JavaScript Object Notation (JSON)](https://www.json.org/), um formato de arquivo que facilita a transferência de dados via navegadores. Por usar HTTP e JSON, as APIs REST não precisam armazenar nem reempacotar os dados, o que as torna muito mais rápidas do que as APIs SOAP.

As APIs SOAP usam protocolos incorporados conhecidos como Web Services Security (WS Security). Esses protocolos definem um conjunto de regras orientado por confidencialidade e autenticação. As APIs SOAP são compatíveis com os padrões definidos pelos dois principais órgãos de padrões internacionais: a [Organização para o Avanço de Padrões em Informação Estruturada (OASIS)](https://www.oasis-open.org/) e o [Consórcio World Wide Web (W3C)](https://www.w3.org/). Elas usam uma combinação de criptografia XML, assinaturas XML e tokens SAML para verificar a autenticação e a autorização. Em geral, as APIs SOAP são apreciadas por ter medidas de segurança mais abrangentes. No entanto, elas também requerem um maior esforço de gerenciamento. Por esses motivos, as APIs SOAP são as mais recomendadas para empresas que lidam com dados confidenciais.

------

## Segurança de API: práticas recomendadas para garantir a segurança das suas APIs

Você provavelmente não guarda suas economias debaixo do colchão. A maioria das pessoas mantém seu dinheiro em um ambiente confiável, geralmente um banco, e usam métodos independentes para autorizar e autenticar pagamentos. A segurança de APIs é assim. É necessário ter um ambiente confiável com políticas de autenticação e autorização.

Algumas das maneiras mais conhecidas de fortalecer a segurança de APIs são:

- **Usar tokens**: estabeleça identidades confiáveis e controle o acesso a serviços e recursos usando [tokens](https://auth0.com/docs/tokens/overview-access-tokens) atribuídos a essas identidades.  
- **Usar criptografia e assinaturas**: criptografe os dados usando métodos como o protocolo TLS descrito acima. Exija o uso de assinaturas para garantir que apenas os usuários certos descriptografem e modifiquem os dados.
- **Identificar vulnerabilidades**: monitore os componentes de sistema operacional, rede, drivers e APIs. Saiba como tudo isso funciona junto e identifique os pontos fracos que podem ser usados para invadir as APIs. Use [sniffers](https://computer.howstuffworks.com/workplace-surveillance2.htm) para detectar problemas de segurança e rastrear vazamentos de dados.
- **Usar cotas e limites**: estabeleça cotas de chamadas de API e monitore o histórico de uso. Um número elevado de chamadas de uma API pode indicar abuso. Isso também pode significar um erro de programação, como realização de chamadas de API em loop infinito. Crie regras de limitação para proteger as APIs contra ataques de DNS e picos de serviço.
- **Usar um gateway de API**: os [gateways de API](https://www.redhat.com/pt-br/topics/api/what-does-an-api-gateway-do) funcionam como o principal ponto de controle do tráfego de API. Um bom gateway permite autenticar o tráfego, bem como controlar e analisar o uso das APIs.

------

## Gerenciamento e segurança de APIs 

Por fim, a segurança de APIs geralmente se resume ao bom gerenciamento. Muitas plataformas de gerenciamento de APIs aceitam três tipos de esquemas de segurança. São eles:

- **Chave de API**, que é uma sequência de caracteres gerada por um único token (isto é, um pequeno dispositivo de hardware que fornece uma informação de autenticação exclusiva).
- **Autenticação básica** (ID/chave de aplicação), que é uma solução de duas sequências de caracteres geradas por token (isto é, nome de usuário e senha).
- **OpenID Connect** (OIDC), que é uma camada de identidade simples em cima da popular estrutura do OAuth (isto é, essa camada verifica o usuário ao obter informações básicas de perfil e usar um servidor de autenticação).

Ao escolher um gerenciador de APIs, saiba quais e quantos desses esquemas de segurança ele pode usar. Além disso, elabore um plano para incorporar as práticas de segurança de APIs descritas acima.

------

## Por que escolher a Red Hat para o gerenciamento e a segurança de APIs? 

Violações de dados são algo assustador, mas você pode tomar algumas medidas para [melhorar a segurança](https://www.redhat.com/pt-br/topics/security/hybrid-cloud-security-approach). As APIs valem esse esforço, basta saber o que deve ser observado. Grande parte desse esforço se resume a adotar [medidas de segurança contínuas](https://www.redhat.com/pt-br/topics/security), fazer as perguntas certas, saber quais áreas precisam de atenção e usar um gerenciador de APIs de confiança. Estamos aqui para ajudar.

Na Red Hat, recomendamos o nosso premiado[ Red Hat 3scale API Management](https://www.redhat.com/pt-br/blog/red-hat-3scale-api-management-and-red-hat-openshift-container-platform-honored-industry-awards). A solução inclui:

- Um gerenciador de APIs que administra aplicações e funções de desenvolvedor
- Um gerenciador de tráfego (gateway de API) que aplica as políticas do gerenciador de APIs
- Um hub provedor de identidades (IDP) compatível com uma ampla variedade de protocolos de autenticação

No gateway de API, o Red Hat 3scale API Management decodifica os tokens com data/hora expirável, verifica se a identificação do cliente é válida e confirma se a assinatura está usando uma chave pública.

[Saiba mais sobre a Red Hat e o gerenciamento de APIs](https://www.redhat.com/pt-br/topics/api/why-choose-red-hat-apis)

### Aprenda mais

- [Introdução às APIs](https://www.redhat.com/pt-br/topics/api)
- [O que é uma API?](https://www.redhat.com/pt-br/topics/api/what-are-application-programming-interfaces)
- [O que é API REST](https://www.redhat.com/pt-br/topics/api/what-is-a-rest-api)
- E-book: [APIs e a linguagem da colaboração corporativa](https://www.redhat.com/pt-br/engage/api-agile-agileintegration-s-201810170209)
- E-book: [O caminho para a adoção de aplicações nativas em cloud](https://www.redhat.com/pt-br/resources/path-to-cloud-native-applications-ebook)
- [Estratégia tecnológica de API aberta para o setor de seguros](https://www.redhat.com/pt-br/resources/open-api-insurance-strategy-brief)
- [Cinco maneiras de implementar o DevSecOps usando a automação da TI](https://www.redhat.com/pt-br/engage/five-ways-implement-s-202107230252)
- [Introdução à segurança de TI](https://www.redhat.com/pt-br/topics/security)
- [Abordagem da Red Hat para a segurança em nuvem híbrida](https://www.redhat.com/pt-br/topics/security/hybrid-cloud-security-approach)
- [O que é malware e como se proteger?](https://www.redhat.com/pt-br/topics/security/what-is-malware)
- [Open banking: o que é, como funciona e quais as vantagens?](https://www.redhat.com/pt-br/topics/open-banking)
- [Novos níveis de eficiência operacional no setor bancário](https://www.redhat.com/pt-br/resources/operational-efficiency-in-banking)
- [Qual é a função de um gateway de API?](https://www.redhat.com/pt-br/topics/api/what-does-an-api-gateway-do)

### Conheça as soluções

[![img](https://www.redhat.com/cms/managed-files/logo-3scale-api-mgmt-green-230x55_0.png)](https://www.redhat.com/pt-br/technologies/jboss-middleware/3scale)

Facilite o compartilhamento, a proteção, a distribuição, o controle e a monetização das APIs para usuários internos ou externos.

[Saiba mais](https://www.redhat.com/pt-br/technologies/jboss-middleware/3scale)

[![img](https://www.redhat.com/cms/managed-files/logo-red-hat-fuse-green-90x55.png)](https://www.redhat.com/pt-br/technologies/jboss-middleware/fuse)

Uma plataforma distribuída de integração nativa em nuvem que conecta suas APIs, seja on-premise, na nuvem e em qualquer outro ambiente de sua escolha.

[Saiba mais](https://www.redhat.com/pt-br/technologies/jboss-middleware/fuse)

### Você pode fazer muito mais com as APIs