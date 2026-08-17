# Performance

## Perspectivas para arquitetar bom software

Dimensões que são necessárias para garantir um bom software

- Performance

- Escalabilidade

- Resiliência

## Métricas para media a performance

- É o desempenho que um software possui para completar determinado workload (ação / tarefa)

- As unidades de medida para avaliarmos a performance de um software são:

    - Latência ou "response time"

    - Throughput: quantidade de tarefas executadas por segundo

- Ter um software performático é diferente de ter um software escalável

### Métricas para medir a performance

São basicamente 2 métricas que precisam mudar para que a performance do software seja melhor.

- Diminuinda a latência:

    - Normalmente em milissegundos - se o tempo for para a casa de "segundos", normalmente o software está lento

    - É afetada pelo tempo de processamento da aplicação, rede e chamadas externas

- Aumentar o throughput:

    - Quantidade de requisições

    - Diretamente ligado a latência

---

### Principais razões para baixa performance

- Processamente ineficiente

- Recursos computacionais limitados

- Trabalhar de forma bloqueante

- Acesso serial a recursos - é o que faz com que as tarefas sejam executadas em ordem, uma após

### Principais formas para aumentar a eficiência

- Escala da capacidade computacional (CPU, Disco, Memória, Rede)

- Lógica por trás do software (Algoritmos, queries, overhead de frameworks)

- Concorrência e paralelismo

- Banco de dados (tipos de bancos, schemas)

- Caching 

---

## Capacidade computacional: escala vertical vs horizontal

- Escala vertical: aumentar a capacidade computacional da máquina

- Escala horizontal: aumento do número de máquinas + load balancer

### Diferença de concorrência e paralelismo

- "Concorrência é sobre lidar com muitas coisas ao mesmo tempo. Paralelismo é fazer muitas coisas ao mesmo tempo" Rob Pike

- Imaginar um web server que recebe 5 requests ao mesmo tempo, para responder demora 10ms cada request.

Em um cenário de concorrência, temos um código que seria bloqueante, que irá resolver todas uma após a outra, e no final o resultado seriam 50ms gastos

Em um cenário de paralelismo, temos um código que é assíncrono, ou seja, ele pode responder de forma paralela, cada request sendo uma thread separada e já resolvendo todas as em simultâneo. O resultado seria 10ms gastos.

---

## Caching

- Cache na borda / Edge Computing (processamento local no celular, ou mesmo em aparelhos gateway próximos sem precisar mandar para o servidor principal)

- Dados estáticos (imagens, css, js estático, etc)

- Páginas web (cacheado na borda, SSG ou SSR)

- Funções internas (fazer caching das funções que são chamadas muitas vezes diretamente no código):
    - Evita reprocessamento de algoritmos pesados

- Objetos (schemas de ORM por exemplo)

### Caching exclusivo vs compartilhado

- Exclusivo: feita na mesma máquina.
    - Possui baixa latência.
    - É duplicado entre nós
    - Problemas relacionados com sessão.

- Compartilhado: cache central.
    - Maior latência
    - Não há duplicação
    - Sessões compartilhadas
    - Banco de dados externo
        - MySQL
        - Redis - mais usado hoje em dia
        - Memcache

### Caching: Edge Computing

- Cache seja realizado mais próximo ao usuário

- Evita a requisição chegar até o Cloud Provider / Infra

- Normalmente arquivos estáticos (já pode colocar na Edge logo no início)

- CDN - Content Delivery Network (Akamai, CloudFlare). Existe cobrança de baixar o arquivo do servidor e também o Midgres (espalhamento do arquivo para os demais locais)

- Cloudflare Workers - permite rodar códigos em tempo real em qualquer lugar da rede, sem precisar de um servidor. É basicamente uma computação em tempo real sem bater no servidor.

- Vercel 

- Akamai