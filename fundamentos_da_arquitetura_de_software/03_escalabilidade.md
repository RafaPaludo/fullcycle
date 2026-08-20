[Referência](https://elemarjr.com/livros/arquiteturadesoftware/)

# Escalabilidade

Escalabilidade é a capacidade de sistemas suportarem o aumento (ou a redução) dos workloads incrementando (ou reduzindo) o custo em menor ou igual proporção.

## Escalabilidade vs Performance

Enquanto performance tem o foco em reduzir a latência e aumentar o throughput, a escalabilidade visa termos a possibilidade de aumentar ou diminuir o throughput adicionando ou removendo capacidade computacional.

## Escalando o software

- Vertical: escala computacional

- Horizontal: quantidade de máquinas + proxy reverso / load balancer

---

## Escalando aplicações - Descentralização

Para escalar horizontalmente, é importante ter em mente que as máquinas são "descartáveis, stateless", no sentido de que possam ser criadas, removidas a qualquer momento sem impactar o restante do sistema.

- Disco efêmero: tudo que for salvo em disco, pode ser apagado no momento que precisar. Usar disco apenas para gravar arquivos temporários.

- Servidor de aplicação vs servidor de assets: ter um servidor específico para as imagens, css, etc. para não ficaram rodando junto com a aplicação. Pois o servidor da aplicação é o que irá "morrer" e depois ser recriado ou replicado.

- Cache centralizado: precisa ter cache em servidor externo específico, para centralizar os dados cacheados.

- Sessões centralizadas: normalmente em um servidor de sessão, que será compartilhado entre as diversas máquinas.

- Upload / Gravação de arquivo: também em outro servidor.

---

## Escalando Banco de Dados

- Aumentando recursos computacionais

- Distribuindo responsabilidades (escrita vs leitura)

- Shards de forma horizontal

- Serverless

### Otimização de Queries e índices

Ter um sistema de APM consegue ajudar a entender melhor como as consultas estão sendo feitas e identificar os possíveis gargalos no sistema.

- Trabalhar com índices de forma consciente

- APM (Application performance monitoring) nas queries

- Explain nas queries

- CQRS (Command Query Responsability Segregation) - separa escrita da leitura

---

## Proxy Reverso

Referências [CloudFlare](https://www.cloudflare.com/learning/cdn/glossary/reverse-proxy/)

Um proxy severso é um servidor que fica na frente dos servidores web e encaminha as solicitações do cliente (por exemplo, navegador web) para esses servidores web.

User /HTTP dominio.com.br               -->               --> Servidor Web 1
User /HTTP dominio.com.br/home          -->               --> Servidor Web 1
User /HTTP dominio.com.br/conta/extrato --> Proxy Reverso --> Servidor Web 2
User /HTTP sub.dominio.com.br           -->               --> Servidor Web 3
User /HTTP sub.dominio.com.br/action    -->               --> Servidor Web 4

Opções de proxy reverso:

- Nginx (Linux)
- HAProxy (HA = High Availability)
- Traefik

TODO: fazer um sistema com NGinx