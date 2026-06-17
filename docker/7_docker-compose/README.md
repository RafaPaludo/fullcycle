## Docker Compose

É um arquivo YML que serve para definirmos alguns passos padrões de trabalho com conteiners.

### Services
Cada conteiner é um service diferente.
Podemos definir:

- Nome
- Imagem docker
- Nome do conteiner
- Redes
- Portas
- ...

### Networks
São as redes que serão criadas e usadas pelos serviços no momento de rodar o comnado UP

Usa o padrão nome rede e driver com o tipo a ser criado:

```
networks:
  laranet:
    driver: bridge
```