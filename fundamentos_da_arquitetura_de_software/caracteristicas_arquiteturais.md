# Características Arquiteturais

Ao criar qualquer tipo de software, é necessário pensar sobre ele antes de começar a programar, além dos requisitos funcionais, também é importante pensar em requisitos não-funcionais, esses normalmente não são explícitos em uma tarefa ou projeto, principalmente pois as pessoas que lideram nem sempre tem as noções técnicas que devem ser consideradas. Resiliência, segurança, escalabilidade, flexibilidade, são exemplos que devem ser considerados.

O livro fundamentos da arquitetura de software mapeia bem esses pontos a se considerar. Existem 3 principais pilares de arquitetura:

- [Operacional](#características-operacionais)

- [Estrutural](#características-estruturais)

- [Cross-cutting](#características-cross-cutting)

---

## Características Operacionais

- Disponibilidade: definir quanto tempo o software deve ficar disponível, se é 24/7 ou outro tipo, além de definir SLA e SLO e combinar um tempo X permitido de indisponibilidade a cada peŕiodo, por exemplo 1hr de indisponibilidade por ano.

- Recuperação de desastres: definir os passos necessários para colocar o sistema no ar novamente. Depois do ocorrido, entender o que fazer para mitigar o mesmo tipo de problema.

- Performance: quanto de performance o sistema deve suportar, será 5k usuarios por segundo ou 10k? Qual a carga de processamento do sistema? Definir o ideal de latência, taxa de erro e throwput.

- Recuperação (backup): definir os passos necessários para fazer backup dos dados. Qual a frequencia do backup? Como é feito o backup?

- Confiabilidade e segurança: principalmente para cenários de pagamento e dinheiro. Páginas de login, sistemas que bloqueiam robos e milhares de requisições por segundo, para não quebrar.

- Robustez: se o sistema se mantem de pé independente dos cenários adversos, seja por conta de ataques, problemas com terceiros sistemas ou falhas locais.

- Escalabilidade: possibilidade de crescer, verticalmente ou horizontalmente. Stateless, 12 fatores. 

---

## Características Estruturais


---

## Características Cross-cutting