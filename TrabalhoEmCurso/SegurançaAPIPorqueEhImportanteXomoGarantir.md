#  Segurança de API: por que é importante e como garantir?

Postado por

Admin Gr1d

Data

03/07/2019

Cada vez mais o mercado segurador busca investir em novas soluções tecnológicas. O objetivo é acompanhar o movimento de transformação digital e aprimorar a experiência dos clientes. É a **tecnologia para seguros** simplificando e otimizando processos.

Contudo, para que recursos como esse sejam oferecidos é preciso investir em tecnologia de ponta. As Interfaces de Programação de Aplicações (APIs), por exemplo, são indispensáveis, já que permitem a comunicação e a integração entre diferentes sistemas. 

E para o desenvolvimento de **API** uma das questões mais importantes é a segurança. Isso porque os ataques e crimes cibernéticos são muito frequentes e vêm sendo refinados. Daí a importância de priorizar os investimentos voltados para a proteção de dados.

De acordo com [pesquisa da Sensedia e IDG Now! sobre O Estado das APIs no Brasil](https://sensedia.com/blog/negocios-digitais/report-estado-das-apis-no-brasil-2017/), embora 75% das empresas brasileiras já usem as APIs, para 85% das grandes e médias empresas a segurança é um fator preocupante. Ou seja, que requer muita atenção de todas as organizações: das PMEs às gigantes nenhuma pode ignorar a importância da segurança das APIs, se quiserem oferecer a melhor experiência ao usuário.

Quer conhecer mais sobre o tema e aprender como aperfeiçoar esse aspecto no mercado de seguros? Continue lendo esse artigo.

**Porque é importante ter APIs seguras**

As APIs são cada vez mais usadas para conectar serviços e transferir dados. Se a segurança tiver comprometida, com APIs disfuncionais, desprotegidas ou hackeadas é como manter as portas abertas para as violações de dados, por exemplo. 

Elas podem, por exemplo, expor publicamente informações pessoais e financeiras, levando a seguradora a enfrentar não apenas as consequências do vazamento de dados, mas também uma crise de imagem que precisará ser muito bem gerenciada.

Por isso, uma das alternativas é investir em APIs que ofereçam mais segurança, com a possibilidade de selecionar as informações de sistema disponíveis para integração com outra plataforma. É importante também garantir o controle de acesso, com mecanismos que indiquem quem acessou os dados do sistema, onde e quando. 

**Quais os fundamentos de segurança de APIs?** 

Considerando a importância de garantir um certo nível de segurança para cada **API**, é importante conhecer os cinco principais pilares que exigem mais atenção na hora de pensar em estratégias para proteger as APIs da seguradora. 

**1. Privacidade**

Prevenir qualquer tipo de exposição ou vazamento de dados sensíveis dos segurados é fundamental. Somente com medidas de segurança bem definidas é possível se proteger de ataques como [*Man-in-the-middle*](https://www.kaspersky.com.br/blog/what-is-a-man-in-the-middle-attack/462/) e [*Eavesdropping*](https://pt.wikipedia.org/wiki/Eavesdropping), por exemplo.

Para garantir a privacidade dos usuários, é importante usar o [SSL/TLS ](https://en.wikipedia.org/wiki/Transport_Layer_Security), que garante a proteção e a criptografia de dados na interação entre um site e um navegador, por exemplo. 

Se não for implementada com cuidado, ela pode abrir brechas de validação de certificado e isso é tudo o que os invasores querem. Dessa maneira, eles têm condições de aplicar ferramentas de interceptação de dados e certificados falsos, obtendo dados como senhas, logins, chaves de **API** e outras informações dos usuários.

Outra dica importante quanto à proteção dos arquivos de log: para protegê-los é necessário garantir sempre o mascaramento de dados sensíveis, como números de cartão de crédito, por exemplo.

**2. Autenticação e Autorização**

Você tem certeza que a pessoa que está tentando acessar sua **API** é quem diz ser? Esse, sem dúvida, é um dos pilares de segurança de APIs mais importantes. Portanto, é fundamental investir em boas práticas de autenticação e autorização de acesso.

Dentre os processos de autenticação simples, um deles é o Basic HTTP, enquanto o OAuth2 e OpenID Connect se evidenciam por serem complementares e mais modernos e seguros.

O padrão OAuth2 vem se destacando como a principal ferramenta de autenticação, que autoriza o acesso a dado recurso, especialmente quando o usuário deve conceder esse acesso. 

**3. Disponibilidade**

Você já imaginou o quanto pode ser frustrante para o usuário acessar um serviço e ver que ele está indisponível? Se ele tiver tentando acionar o seguro, por exemplo, será difícil reparar essa experiência. Por isso, é fundamental que as APIs estejam acessíveis e disponíveis, com um ótimo desempenho.

Uma das estratégias para garantir a disponibilidade é adotar medidas de segurança, protegendo-se de [ataques distribuídos de negação de serviço (DDoS)](https://pt.wikipedia.org/wiki/Ataque_de_negação_de_serviço), por exemplo, [Buffer Overflow](https://www.welivesecurity.com/br/2014/11/11/o-que-e-e-como-funciona-o-buffer-overflow/) ou até mesmo injeções de códigos maliciosos.

São ações protetivas que você pode adotar: 

- Políticas de Rate Limiting / Throttling
- JSON / XML Threat Protection
- Limites de tamanho de Payload
- IP Filtering (Blacklists e Whitelists)

Outro ponto importante é monitorar o tráfego nas APIs, configurando alertas para identificação de comportamento malicioso.

**Como melhorar a segurança das APIs?**

Até aqui foi possível compreender a relevância da segurança da informação, especialmente das APIs, na **tecnologia para seguros**. A questão é: como garantir a segurança no desenvolvimento e na integração das interfaces? É preciso manter um ambiente confiável com boas práticas bem claras e definidas. Veja, a seguir, algumas delas:

- **Adotar o uso de tokens**: é fundamental criar identidades confiáveis e controlar o acesso a serviços e recursos usando tokens atribuídos a cada identidade. 
- **Usar a criptografia e assinaturas**: com métodos como o protocolo TLS para criptografar os dados dos usuários. Além disso, exija assinaturas para cada um. Assim é possível garantir que somente aqueles autorizados podem descriptografar e modificar os dados.
- **Estabelecer controle do tráfego:** para tanto, use um *gateway* de **API**. Ele permite autenticar o tráfego, bem como controlar e analisar o uso das APIs.
- **Monitorar o histórico de uso:** ao usar cotas de chamadas de **API** é possível identificar se a utilização é padrão ou há um uso exagerado dela. O acompanhamento pode indicar, por exemplo, um erro de programação como chamadas em loop infinito. Outra prática inteligente é definir regras de limitação para proteger as APIs de ataques de DNS e picos de serviço.

A segurança da informação precisa ser uma das prioridades das empresas do mercado de seguros que desejam crescer. Quer saber mais sobre o tema? Continue acompanhando o Trends!