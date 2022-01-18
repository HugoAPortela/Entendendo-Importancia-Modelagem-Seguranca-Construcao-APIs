[ das APIs](https://vertigo.com.br/category/mundo-das-apis/)

 18 min leitura

# As melhores práticas de segurança para o uso de API

- ![Marketing Vertigo](https://secure.gravatar.com/avatar/def28d13553d7d5f7d14468bab26a8a0?s=50&d=mm&r=g)
- Autor :Marketing Vertigo
- Publicado :  novembro 30, 2020

![img](https://hml.vertigo.com.br/wp-content/uploads/2020/11/seguranca-aplicacoes.png)

Com as organizações iniciando a transformação digital, o primeiro passo para projetar e executar suas iniciativas costuma ser a adoção da [abordagem de API](https://vertigo.com.br/como-fazer-api-uma-de-sucesso/). Isso junto com as práticas Ágeis e de DevOps são o cerne da transformação. As APIs fornecem uma demarcação clara para implementação e condução de DevOps, o que traz agilidade aos lançamentos de software.
No entanto, é necessário garantir que as APIs sejam validadas e a aplicação não esteja lenta. Com a metodologia ágil, surge o desafio de manter todos os stakeholders em sincronia. Então, para continuar atualizado é preciso verificar e aplicar as proteções de segurança de maneira dinâmica.
Se não houver atenção nessas práticas, a agilidade do DevOps pode resultar em APIs ocultas, fora do alcance da TI corporativa. Isso abre brecha para o cibercrime: de acordo com Mark O’Neill, Vice President Analyst na [Gartner](https://www.gartner.com/), o uso abusivo de APIs será o vetor de ataque mais frequente em 2022.
Ou seja, mesmo que todo o seu uso de API seja somente interno, ainda podem surgir problemas de segurança. Pensando nisso, reunimos uma lista de práticas recomendadas para proteger uma API ou serviço web. Continue lendo nosso artigo e descubra!

## Use HTTPS

A época do HTTP padrão já passou! Com navegadores sinalizando URLs que não usam camada segura, é hora de fazer o mesmo com sua API. HTTPS usa Transport Layer Security (TLS) para criptografar o tráfego, isso inclui toda a comunicação entre cliente e servidor.
Para sua API, isso significa que o conteúdo enviado é protegido por terceiros, mas o mais importante é que as credenciais de acesso estão protegidas.

## Autenticação

Por falar em credenciais de acesso, a maneira mais simples de evitar o uso inesperado de sua API é garantir a autenticação adequada. A autenticação é como você permite ou impede o acesso à API. Mesmo aquelas disponíveis publicamente ou de uso gratuito devem ter uma estratégia de autenticação.
Assim, é possível limitar ou remover aqueles que abusam da API e também proteger seus usuários, dando-lhes a capacidade de redefinir suas credenciais caso seja necessário.

## Autorização

A autorização caminha junto com a autenticação: enquanto a primeira se preocupa com quem é o usuário de sua API, a segunda se concentra em que ele tem acesso ou quais ações pode executar. Por exemplo, quem possui plano de assinatura gratuito do seu serviço só pode ter autorização para acessar um subconjunto da sua API.
Outro exemplo é o login social: em integrações como essa, o usuário autoriza sua aplicação a ler os dados de seu próprio perfil na plataforma social.

## Segurança em recursos e endpoints

É comum proteger um endpoint ou um conjunto deles através de autorização. Uma abordagem de transformação digital também visa proteger os recursos individuais. 
Isso evita que uma autorização mal configurada no nível do endpoint alcance dados importantes, significando que os próprios não são restritos pelo tipo de usuário, mas, em vez disso, pelos controles de recursos de quem pode ou não visualizá-los.

## Taxa limite (*Rate Limit*)

Quando pensamos em segurança, geralmente lembramos de acesso inadequado, mas também pode ser útil pensar como gerenciamento de recursos. Criar um rate limit é uma técnica para proteger seus recursos financeiros através da limitação do uso de uma API, mas também garantir que seus servidores não sejam sobrecarregados por uma enxurrada de solicitações em simultâneo não desejadas.
Muitas relações de limitação de taxa são baseadas no tempo, mas também podem ser configuradas para um período de faturamento ou um procedimento intermitente com objetivo de limitar grandes fluxos de solicitações. Se você já se deparou com o código de status HTTP 429, então você experimentou limitação de taxa.

## Validar e higienizar a entrada

Um dos pontos de ataque mais antigo é o campo de entrada. A maneira como os dados são acessados pode ter mudado, mas não a necessidade de validar qualquer entrada do usuário.
A validação *client side* é útil para evitar erros e melhorar a experiência do usuário, mas sua API também precisa validar e higienizar todas as entradas antes de rodar.
A higienização remove malwares ou códigos maliciosos e a validação garante que os dados atendam aos critérios necessários que podem ser por tipo, forma ou até mesmo por fatores, como a estrutura da senha.

## Exponha apenas o que é necessário

Pode ser tentador pegar um atalho e mapear diretamente os modelos de dados para endpoints, mas este caminho pode acabar fornecendo respostas desnecessariamente detalhadas, o que aumenta o uso da largura de banda e expõe dados os quais os usuários não precisam ter acesso.
Por exemplo, considere um endpoint “/user” que retorna ao perfil do usuário. Ele pode precisar de algumas informações básicas, mas não da senha ou dos níveis de acesso.

## Configurar mensagens de erro

Além de limpar os dados que vão para sua API, é preciso limpar também as informações que saem dela. As mensagens de erro desempenham um papel fundamental para ajudar os usuários a entender que ocorreu um erro, mas é preciso certificar-se de não vazar dados confidenciais.
Fornecer detalhes sobre a estrutura de seu código interno aos usuários finais pode abrir brechas para cibercrime. Certifique-se de configurar mensagens de erro para fornecer informações suficientes somente para ajudar os usuários a relatar problemas, mas não o bastante para expor o funcionamento interno da sua aplicação ou dados confidenciais.

## Não exponha informação sensível

Para desenvolver a proteção de dados confidenciais, certifique-se de não expor detalhes em JSON web tokens (JWTs) ou cookies. O JWT traz a ilusão de ser seguro, mas pode ser facilmente decodificado.
Por isso, é preciso evitar incluir informações do usuário que possam ser usadas para acessar sua aplicação. O mesmo conselho vale para URLs: certifique-se de que as strings de consulta não estejam expondo detalhes confidenciais.

## Avalie suas dependências

Atualmente uma boa parte de cada codebase contém bibliotecas, middleware e uma variedade de dependências de fontes externas. Embora seja seguro presumir que os pacotes populares são battle-tested, isso não significa que eles estejam completamente protegidos contra vulnerabilidades.
Certifique-se de avaliar suas dependências: elas são bem mantidas? Você está usando a última versão? Existe um histórico de problemas? E, talvez o mais importante: você realmente precisa de uma biblioteca de terceiros para o que está fazendo?

## Permita que os usuários rastreiem e redefinam as chaves de autenticação

Uma maneira adicional de melhorar a segurança de sua API é permitir que os usuários redefinam suas credenciais e monitorem seu próprio uso. Inclusive, não permitir esta ação é um erro comum.
Se um consumidor de sua API expõe sua chave acidentalmente ou se ela é interpretada de forma maliciosa, o problema agora afeta diretamente sua API, não só o usuário. Para isso não acontecer, crie um meio para que eles consigam gerenciar o próprio acesso.

## Padronize a autenticação em seus serviços

Assistimos grandes players como Google, Microsoft e Amazon padronizarem o processo de autorização e autenticação para suas APIs. Siga o exemplo deles e considere uma maneira centralizada de fazer isso, como usar uma [API gateway](https://vertigo.com.br/api-gateway-ou-api-management/), por exemplo, ou um ponto de entrada dedicado para lidar com solicitações de autenticação.

## Monitore suas APIs com Kong Manager

Utilizamos a ferramenta Kong Manager em alguns projetos aqui na Vertigo e consideramos ser a solução ideal para gerenciar as suas APIs com segurança. Desenvolvida com uma abordagem voltada para o consumidor, possui a usabilidade necessária para que o usuário se sinta envolvido em seus processos com facilidade.
Neste artigo aprendemos que, conforme as arquiteturas de software se tornam mais complexas, as organizações precisam de uma maneira mais fácil de gerenciar seus serviços. A Kong Manager ajuda na organização de equipes, ajuste de políticas e monitoramento do desempenho com apenas alguns cliques.
Afinal, seus plugins empresariais permitem implementação instantânea de políticas criadas para escala global. Já sua Visual API Analytics monitora a saúde da plataforma e as transações da API de microsserviços que a atravessam.

![img](https://vertigo.com.br/wp-content/uploads/2020/11/testesteste.png)

Com esta ferramenta você tem a possibilidade de agrupar suas equipes, serviços, plugins, gerenciamento de consumidor e o que mais precisar, personalizado exatamente da maneira como deseja:

- Crie rotas e serviços;
- Ative ou desative plugins em segundos;
- Visualize a integridade de todo o cluster em um único painel de vidro usando painéis intuitivos e personalizáveis.

Para garantir a segurança das suas APIs é fundamental que haja um suporte aos produtos oferecidos na nuvem. A Kong Manager permite sua unificação, o que proporciona flexibilidade na criação de novos features interativos sem o receio de bloqueio. Também podemos mencionar outros benefícios, como:

### Gestão dinâmica

É possível ativar ou desativar plugins para ajustar políticas de serviços, rotas e consumidores de forma instantânea. Além disso, há a integração entre desenvolvedores internos e externos.

### Melhor governança

Com a Kong você organiza suas equipes, serviços e consumidores de maneira lógica e eficiente. E, para mais segurança, é possível limitar o acesso para as pessoas certas com controles totalmente personalizáveis baseados em funções (RBAC).

### Desempenho otimizado

A Kong Manager realiza o monitoramento da integridade de sua implantação de maneira global ou a nível granular, com isso é possível identificar e resolver problemas de desempenho em tempo real.

## Concluindo

A flexibilidade da Kong Manager permite rodá-la em qualquer ambiente, seja nuvem pública ou privada. Também oferece a capacidade de aplicar especificações de API aberta para seus microsserviços em execução. Com ela as organizações evitam o uso abusivo das API, reforçando as práticas recomendadas.
Se sua API depende de APIs de terceiros, considere a implementação de uma solução como a Kong Manager para permitir que você rastreie, observe, reaja e receba alerta quando alguma API não estiver funcionando conforme o esperado.
Somos parceiros oficiais da Kong e especialistas em Kong Enterprise Edition (EE), atuando na implementação em grandes projetos tecnológicos de diversos segmentos como indústria, governo, serviços financeiros, bens de consumo e mais.
Empresas como Icatu Seguros, Ipiranga, ABInBev e Ministério Público do Rio de Janeiro se beneficiaram com nossas estratégias de integração de sistemas e gerenciamento de APIs.
Conte conosco para projetar, criar e gerenciar seus projetos digitais, obter aplicações móveis mais ágeis, desenvolver novos modelos de negócios, monetizar seu empreendimento digital, conectar seu ecossistema e levar a sua empresa ao sucesso no mercado!
Para saber mais sobre integração de sistemas, gerenciamento e segurança de APIs e como isso tudo pode ajudar os seus negócios, [fale com nossos especialistas](https://vertigo.com.br/contato/)! Teremos prazer em ajudá-lo.