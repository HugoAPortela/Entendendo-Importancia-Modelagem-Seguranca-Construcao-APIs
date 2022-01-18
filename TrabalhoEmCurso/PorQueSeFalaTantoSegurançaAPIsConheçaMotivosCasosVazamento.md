# Por que se fala tanto de Segurança de APIs? Conheça os motivos e casos de vazamento

[![David Ruiz](https://miro.medium.com/fit/c/56/56/1*qZlv69AGI92EpBLhXMZxVg.jpeg)](https://medium.com/@i9dvdr?source=post_page-----74a9b4df8577--------------------------------)

[David Ruiz](https://medium.com/@i9dvdr?source=post_page-----74a9b4df8577--------------------------------)

[Nov 28, 2019·7 min read](https://medium.com/@i9dvdr/por-que-se-fala-tanto-de-segurança-de-apis-conheça-os-motivos-e-casos-de-vazamento-74a9b4df8577?source=post_page-----74a9b4df8577--------------------------------)







![img](https://miro.medium.com/max/1400/1*sEt2TIofjPTaA9EcR-aXWA.jpeg)

Diversas empresas e outros tipos de organizações tem se beneficiado do uso de APIs, especialmente pela possibilidade de conectar serviços e integração de dados. Entretanto, há algo que você não pode deixar de lado quando está trabalhando com APIs: a segurança e integridade dos dados. Afinal, a segurança é essencial para a boa execução de uma API.

Caso uma API apresente problemas, esteja desprotegida ou seja hackeada, muito provavelmente você terá seus dados violados. O resultado é a exposição pública de dados financeiros, médicos ou pessoais. Uma verdadeira invasão de privacidade.

Claro que já houve avanços nos últimos anos no que diz respeito à segurança de APIs, mas ainda sim ataques às barreiras de proteção existem. Por isso, seja você um desenvolvedor, alguém que usa ou fornece APIs, atente-se à segurança de seus dados.

É preciso esclarecer que os níveis de importância varia de acordo com o tipo de dado, o que significa que cada informação deve ser protegida de uma forma. A abordagem de segurança de API deve levar em consideração o tipo de dados que está sendo transferido.

Se você faz uso de APIs em sua empresa para se conectar a aplicações de outras organizações fique atento a como tais aplicações retornam seus dados para internet. Uma invasão de dados pode ter diferentes tamanhos de proporções.

A sigla IoT tem aparecido cada vez mais. Ela significa Internet das Coisas e é muito provável que você ou algum conhecido já tenha contato com ela. Estou falando daquela tecnologia que consegue interconectar diferentes objetos do seu cotidiano por meio da internet.

Dessa forma, se você quisesse poderia muito bem, por exemplo, conectar seu smartphone a geladeira e ser notificado dos alimentos que precisa comprar no supermercado.

Muito prático não é mesmo?

**A estimativa é que até 2020 haja 50 bilhões de dispositivos conectados pela IoT!**

Imagine a praticidade e funcionalidade a partir dos dispositivos conectados. Imagine o volume de dados que é transmitido com isso!

# **E QUAL A RELAÇÃO ENTRE A SEGURANÇA DE APIs E IOT?**

A ascensão da Internet das Coisas sofre influência de uma série de tecnologias facilitadoras, dentre elas RFID, IPv6, Big Data e interfaces de programação de aplicações (APIs).

**As APIs estão intimamente relacionadas com a IoT, já que são uma da peças-chave para a conexão de dispositivos à internet** e possuem protocolos fáceis de implementar e leves recursos de computação. Quanto mais falamos de integração e inter-conectividade, mais a temática de APIs se torna relevante.

A revolução da Internet das Coisas tem levado cada vez mais empresas a criar APIs que suportem os dispositivos conectados. Logo as APIs são de enorme contribuição para a democratização de objetos conectados, tanto que essa relação se faz, ao mesmo tempo, forte e necessária. Uma das consequências é o crescimento e desenvolvimento de uma Economia de APIs.

Agora é que a questão se complica. Lembra da sua geladeira conectada ao seu celular? Vamos supor alguém viole seus dados e descubra o que você guarda em sua geladeira, não parece nenhuma informação ultrassecreta e que irá prejudicá-lo.

O que acontece quando essa pessoa utiliza a mesma API, aquela que ajuda na conexão de sua geladeira e smartphone, para descobrir onde você mora?

**O fato das APIs estarem envolvidas diretamente na comunicação entre diversos sistemas é motivo suficiente para que você se preocupe com a integridade de seus dados** enquanto estes são transferidos para outros dispositivos.

Garantir a segurança de suas APIs é garantir que somente aplicativos e desenvolvedores autorizados por você possam se comunicar com suas APIs e ter acesso aos dados transferidos por elas.

Entretanto quando falo de segurança de APIs não é apenas na sua relação com IoT que você deve se preocupar. A Internet das Coisas é apenas uma das peças que a devemos ficar atentos quando o assunto é a proteção de dados sensíveis que trafegam pelas APIs. Afinal grandes empresas também sofreram ataques às suas APIs.

# **FIQUE POR DENTRO DE ALGUNS CASOS ENVOLVENDO SEGURANÇA DE APIS**

O quanto uma empresa pode sair prejudicada pelo vazamento de dados sensíveis de seus clientes? 10 milhões é o valor aproximado da multa que empresa de telefonia TIM terá de pagar em decorrente de uma falha na segurança de sua API. O processo foi aberto pela Secretaria Nacional do Consumidor (SENACON), do Ministério da Justiça e Segurança Pública.

O vazamento foi informado em abril deste ano por Felipe Payão no [TecMundo](https://www.tecmundo.com.br/seguranca/140322-tim-negocia-vazou-dados-pessoais-dividas-milhares-clientes.htm). A origem do problema estava na plataforma TIM Negocia. Nela clientes (pessoa física ou jurídica) podem conferir se têm dívidas com a operadora e resolver quaisquer pendências financeiras.

O vazamento afetou milhares de clientes, que tiveram informações como nome completo, CPF, número de celular e data de nascimento expostos pela operadora.

O hacker Krypt0nsh3ll, responsável por enviar os dados sensíveis de 48 mil clientes a Felipe Payão, afirmou que o acesso foi possível graças a uma API exposta da TIM. De acordo com o hacker também era possível ler o histórico do atendimento via chat.

Outro caso mais recente envolveu o portal Meu Vivo. No início de novembro o [Olhar Digital](https://olhardigital.com.br/fique_seguro/noticia/-exclusivo-falha-de-seguranca-expoe-dados-de-24-milhoes-de-usuarios-da-vivo/92520) divulgou uma uma falha de segurança no portal de serviços da operadora que deixava expostos dados de 24 milhões de assinantes.

A falha foi identificada pelo grupo de pesquisadores “WhiteHat Brasil”. O grupo explicou que foi utilizada a técnica de “raspagem de dados” para acessar dados sensíveis (nome completo, endereço, data de nascimento, RG, CPF, e-mail, nome da mãe e número de telefone), burlando a criação de tokens com um software que os pesquisadores identificaram a falha.

No caso da Vivo, a exposição de dados atingiu tanto clientes da operadora quanto interessados em assinar algum dos serviços.

A falha da Vivo não foi a primeira divulgada pelo grupo “WhiteHat Brasil”. Em outubro deste ano, os pesquisadores já haviam feito uma comunicado exclusivo ao Olhar Digital sobre uma grave brecha na segurança do portal de serviços “Minha Claro Residencial”. Segundo o grupo mais de 8 milhões de clientes tiveram seus dados expostos na internet.

O “WhiteHat Brasil” explicou que o acesso aos dados de clientes cadastrados se deu da seguinte forma: primeiro o sistema da operadora gera uma “token” para validar o acesso do usuário, em seguida é possível identificar facilmente um link contendo o CPF do cliente no final. A partir de um programa básico é possível que alguém tenha acesso a todos os dados de usuários cadastrados no “Minha Claro Residencial”.

# **AS AMEAÇAS DE SEGURANÇA DE DADOS RELACIONADAS ÀS APIS**

As APIs são um dos alvos prediletos de hackers, principalmente pelo elevado volume de dados sensíveis e quantidade significativa de usuários que podem ser atingida. Para que você tenha uma ideia de como tais ataques podem ocorrer, vou citar alguns exemplos de ameaças à segurança de seus dados:

## **Injeção**

Esse tipo de ataque é comum e de fácil detecção, entretanto não o subestime, pois ele pode trazer consequências severas. O ataque por injeção ocorre quando dados maliciosos, no formato de comandos ou consultas, são enviados a um “interpretador”, levando a habilitação de ações indesejadas.

A melhor maneira de evitar esse ataque é checando o tráfego de dados das suas APIs e vendo se há comandos do tipo SQL, JSON, XML. Você pode fazer isso por meio de um API Management. Quanto ao “interpretador” evite usá-lo.

## **Quebra de Autenticação**

É um ataque comum às APIs que resulta em acessos não autorizados. Diferente de um ataque de injeção, uma quebra de autenticação é mais complicada de se detectar. Para não ter uma dor de cabeça com ela, você precisa de uma comunicação segura com two way SSL e padrões de autenticação OAuth.

## **Acesso a dados sensíveis**

**Dados sensíveis são informações privadas**. Você provavelmente não gostaria que estas fossem compartilhadas na internet. Um dado sensível pode ser seu nome completo, endereço de residência ou trabalho, número de telefone, CPF, RG e número de cartão de crédito. Já deu para perceber que as consequências da exposição de tais dados seria grave.

O melhor é evitar que estas informações estejam gravadas em algum ambiente virtual não criptografado. Para mitigar quaisquer situações de vulnerabilidade tenha um canal de comunicação criptografado e use o two-way SSL.

O auto-completar de formulários pode parecer mais simples e prático, mas ele também deixa suas informações mais vulneráveis, por isso o desabilite. E claro, uma das dicas mais importantes: **não armazene nenhum dado sensível sem necessidade**.

## **Falhas de configurações de segurança**

Quando suas configurações de seguranças não operam corretamente, outros usuários podem executar ações indesejadas. Sua detecção é simples, porém é necessário garantir que o problema seja eliminado por completo. A permanência de falhas nas configurações de segurança pode trazer impactos técnicos sérios.

Do mesmo modo que sua detecção é simples, sua prevenção também é, basta realizar varreduras periódicas e automáticas. Outra forma de cuidar de seus dados é a partir de uma arquitetura que permita a separação segura de componentes.

## **Ataques do tipo XML External Entity** (onde as informações contidas em XMLs antigos podem ser acessadas indevidamente)

Entidades externas de arquivos XML, chamadas de External Entities (XXE), compõem uma das principais ameaças. Para evitar extração de dados e ataques de DoS, ocasionados por falhas de processadores antigos, mantenha sempre seus processadores atualizados e aplique as correções necessárias. Dessa forma, você se previne contra XMLs vulneráveis.

Outras maneiras de evitar esse ataque é utilizando um API Management e assim seu módulo de Security Gateway será habilitado para evitar esse problema.

A gravidade dos danos e os ataques que sua API pode sofrer vão depender que como ela foi criada e da sua finalidade. Ela pode muito bem ter sido desenvolvida para ambientes internos ou para usuários externos a sua empresa. É importante analisar quais os possíveis riscos e implementar uma política de segurança de APIs seguindo as características delas.