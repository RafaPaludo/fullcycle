# Características Arquiteturais

Ao criar qualquer tipo de software, é necessário pensar sobre ele antes de começar a programar, além dos requisitos funcionais, também é importante pensar em requisitos não-funcionais, esses normalmente não são explícitos em uma tarefa ou projeto, principalmente pois as pessoas que lideram nem sempre tem as noções técnicas que devem ser consideradas. Resiliência, segurança, escalabilidade, flexibilidade, são exemplos que devem ser considerados.

O livro fundamentos da arquitetura de software mapeia bem esses pontos a se considerar. Existem 3 principais pilares de arquitetura:

- [Operacional](#características-operacionais)

- [Estrutural](#características-estruturais)

- [Cross-cutting](#características-cross-cutting)

---

## Características Operacionais

São coisas mas gerais daquilo que pode gerar problemas além do software em si. 

- Disponibilidade: definir quanto tempo o software deve ficar disponível, se é 24/7 ou outro tipo, além de definir SLA e SLO e combinar um tempo X permitido de indisponibilidade a cada peŕiodo, por exemplo 1hr de indisponibilidade por ano.

- Recuperação de desastres: definir os passos necessários para colocar o sistema no ar novamente. Depois do ocorrido, entender o que fazer para mitigar o mesmo tipo de problema.

- Performance: quanto de performance o sistema deve suportar, será 5k usuarios por segundo ou 10k? Qual a carga de processamento do sistema? Definir o ideal de latência, taxa de erro e throwput.

- Recuperação (backup): definir os passos necessários para fazer backup dos dados. Qual a frequencia do backup? Como é feito o backup?

- Confiabilidade e segurança: principalmente para cenários de pagamento e dinheiro. Páginas de login, sistemas que bloqueiam robos e milhares de requisições por segundo, para não quebrar.

- Robustez: se o sistema se mantem de pé independente dos cenários adversos, seja por conta de ataques, problemas com terceiros sistemas ou falhas locais.

- Escalabilidade: possibilidade de crescer, verticalmente ou horizontalmente. Stateless, 12 fatores. 

---

## Características Estruturais

São coisas mais ligadas ao software em si.

- Configurável: variável de ambiente para conexão fácil em novos DBs, fácil de trocar APIs no software, Feature Flags

- Extensibilidade: aplicação tem que crescer de forma que terceiros possam "plugar" suas funcionalidades. 

- Fácil instalação: padronizar ambientes para ficar fácil de fazer deploy e rodar localmente. 

- Reuso de componentes: principalmente em sistemas monolíticos já é mais fácil. Em sistemas distribuídos, equipes podem acabar criando coisas parecidas.

- Internacionalização: pensar em políticas de preço no backend, layout no frontend.

- Fácil manutenção: aprender SOLID, adição de novas features, correção de bugs, testes.

- Portabilidade (diversos DBs): conseguir trocar de banco ou coisas críticas de forma simples.

- Fácil suporte (logs, debugging, alertas): ter as métricas de forma rápida.

---

## Características Cross-cutting

- Acessibilidade: saber o público que acessa a aplicação, tamanho ícones e fontes, sons, imagens. 

- Processo de retenção e recuperação de dados (quanto tempo os dados serão mantidos): o que precisa ser guardado ou podem ser excluídos.

- Autenticação e Autorização: complexo principalmente em arquiteturas distrubuídas

- Legal: LGPD, manter os dados

- Privacidade: LGPD, minimizar problemas com vazamento de dados.

- Segurança: desde a borda, antes do usuário acessar a aplicação, **web file**, identifcar se robos estão tentando acessar aplicação, SQL Injection, etc.

- Usabilidade: navegação do usuário, tracking de eventos, organização das APIs, documentação, padrões e contratos claros.