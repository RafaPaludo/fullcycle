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

