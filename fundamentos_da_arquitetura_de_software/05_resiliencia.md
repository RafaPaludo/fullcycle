# Resiliência

É um conjunto de estratégias adotadas intencionalmente para a **adaptação** de um sistema quando uma falha ocorre.

Ter estratégias de resiliência nos possibilita minimizar os riscos de perda de dados e transações importantes para o negócio.

## Proteger e ser protegido

Um sistema em uma arquitetura distribuída precisa adotar mecanismos de autopreservação para garantir ao máximo sua operação com **qualidade**.

Um sistema não pode ser "egoísta" ao ponto de realizar mais requisições em um sistema que está falhando.

Um sistema lento no ar muitas vezes é pior do que um sistema fora do ar. (Efeito dominó)

- Quando um sistema está com dificuldade em responder e diversos outros estão requisitando, gera um efeito em cascata, pois os demais começam a ficar lentos também na espera da resposta desse sistema com problema. Por isso as vezes vale mais a pena ter estratégia de retornar 500 para toda request a fim de evitar essa lentidão generalizada em todos.

Efeito dominó:
App A -> App B -> App C (lento)
App A -> App B (lento) -> App C (lento)
App A (lento) -> App B (lento)-> App C (lento)

Quando o sistema identifica lentidão e já retorna isso:
App A -> App B -> App C (lento retorna 500)
App A -> App B -> App C (lento retorna 500)
App A -> App B -> App C (lento retorna 500)

---

## Health Check

Sem sinais vitais não é possível saber a "saúde" do sistema

Um sistema que não está saudável possui uma chance de se recuperar caso o tráfego pare de ser direcionado a ele temporariamente (self healing)

Health check de qualidade. Ao invés de retornar apenas um 200, fazer uma análise correta do status, verificar banco, verificar últimas requests, etc para saber se o sistema de fato está estável com as demandas que ele deve fazer.

---

## Rate limit

Fazer um teste de stress para entender até onde que o sistema aguenta, definir os valores máximos que ele suporta. Por exemplo, entendeu que o sistema aguenta 100 req/s, caso o fluxo esteja muito acima disso, já começa a responder erro 500 por exemplo, para garantir a integridade dos demais sistemas.

- Protege o sistema baseado no que ele foi projetado para suportar

- Preferência programada por tipo de client: definir qual a quantidade que cada cliente pode fazer em um determinado tempo. Isso possibilita priorizar clientes vitais para a empresa e definir valores bem baixos para outros.

---

## Circuit Breaker

- Protege o sistema fazendo com que as requisições feitas para ele sejam negadas. Ex: retornar 500

- Circuite fechado = Requisições chegam normalmente

- Circuito aberto = Requisições não chegam ao sistema. Erro instantâneo ao client

- Meio aberto = Permite uma quantidade limitada de requisições para verificação se o sistema tem condições de voltar ao ar integralmente.

---

## API Gateway

É uma camada que recebe as requisições e a partir das necessidades da aplicação, pode inserir dados, negar a comunicação, etc. podem ser aplicadas diversas regras para definir se continua, barra ou condiciona para outra parte.

- Garante que requisições "inapropriadas" cheguem até o sistema. Ex: usuário não autenticado.

- Implemnenta políticas de Rate Limiting, Health Check, etc.

- Exemplos: Kong

---

## Service Mesh

- Controla o tráfego da rede

- A comunicação entre os serviços ao invés de ser direta, é feita através de proxies intermediárias. 

- Evita implementações de proteção pelo próprio sistema.

- mTLS = Mutual TLS = Certificados de segurança compartilhados entre os servidores e clientes.

---

## Comunicação assíncrona

- Evita perda de dados, pois não depende da ordem das requisições.

- Não há perda de dados no envio de uma transação se o server estiver fora

- Servidor pode processar a transação em seu tempo quando estiver online

- O intermediário nesse processo é geralmente chamado de Message Broker, ele só armazena a requisição e depois passa para o próximo servidor, não se preocupa com os dados enviados.

- Entender com profundidade o message broker / sistema de stream.

- Kafka, RabbitMQ, Amazon SQS, etc.

---

## Garantias de entrega: Retry

A ideia aqui é que o client faça novas tentativas para enviar a requisição se ela falhar. 

O problema é que se existirem váios clients enviando a mesma quantidade de requisições e o servidor não conseguir lidar, independe o tempo de retry, pois sempre vão ser enviadas x requisições e o servidor não conseguirá processar novamente, e assim por diante.

Para tentar mitigar isso, existe algumas opções:

- Exponential backoff: são os tempos que o client vai esperar para tentar enviar a requisição de novo. O tempo começa em um valor pequeno e aumenta de forma exponencial, por exemplo 2s, 4s, 8s, 16s, 32s, 64s, 128s...

- **Exponential backoff Jitter**: adiciona um pequeno ruído nos tempos de retry, para que as chamadas não sejam exatamente no mesmo momento, por exemplo:
    - Client 1: 2.1s, 4.5s, 8.01s, 16.39s, 32.79s, 65.58s
    - Client 2: 2.2s, 4.6s, 8.22s, 16.44s, 32.88s, 65.76s
    - Client 3: 2.09s, 4.18s, 8.36s, 16.12s, 32.24s, 64.48s

Existem diferentes algoritmos de Jitter, mas todos eles são muito melhores que apenas o retry.

---

## Garantias de entrega: Kafka

Cada Message Broker possui suas especificidades. Mas de forma geral, eles implementam formas de garantir o envio das mensagens para os clientes, tendo custos e velocidades diferentes.


- Nesse caso o cliente (Producer) quer que envie mesmo sem esperar a confirmação da entrega, ela pode nem ser enviada (fire and forget)
Producer -> Ack 0 -> Broker A (Leader)
            (none)   Broker B (Follower)
                     Broker C (Follower)


- Nesse caso o clinte (Producer) quer que somente o Leader confirme que recebeu a mensagem, mas ainda corre o risco de ele dizer que recebeu e logo em seguida "morrer" e não entregar.
Producer -> Ack 1 -> Broker A (Leader)
           (Leader)  Broker B (Follower)
                     Broker C (Follower)

- Nesse caso o clinte (Producer) quer que todos os brokers confirmem que receberam a mensagem, garantindo que se um caia, os demais poderão enviar.
Producer -> Ack 0 -> Broker A (Leader) v
            (ALL)    Broker B (Follower) v
                     Broker C (Follower) v

--- 

## Situações complexas

- O que acontece se o message broker cair?

- Haverá perda de mensagens?

- Seu sitema ficará fora do ar?

- Como garantir resiliência?