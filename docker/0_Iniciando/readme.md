## Objetivos

- O que são containers
- Como funcionam os Containers
- Como o Docker funciona
- Principais comandos do Docker
- Dockerfile
- Trabalhando com imagens Docker

---

Namespaces = A partir da ideia de Namespaces, que são processos pai + processos filhos que rodam separados de outros processos no SO, tem-se o modelo de contâiner.

Cgroups = controla os recursos computacionais dos containers. Dessa forma definimos a quantidade de memória, cpu, etc aquele processo pode utilizar, para não usar todo o recurso do host e interfirir nos demais processos (containers).

File System = OFS (Overlay File System) é a ideia de trabalhar com camadas, quando atualizar alguma dependência ou pacote do container, ele só atualiza aquilo que foi mudado. É basicamente a diferença entre VM e o container em si.

Imagens = uma imagem pode conter diversas dependências, e se necessário é possível mudar alguma dependência e buildar a imagem novamente.

## Dockerfile

É um arquivo declarativo para CONSTRUIR IMAGENS, ele define como a imagem deve ser montada. Idealmente deveria começar com uma imagem vazia, porém na prática é importada uma imagem já pronta com algumas coisas padrão.

FROM: Nome da Imagem

RUN: comandos - ex: apt get install ...

EXPOSE: 8000 - expor portas específicas

## Arquitetura do Docker

Docker Client: (usa o daemon API)
  Containers - Run, Pull, Push, Volumes, Network

Docker Host:
  Volumes (persiste os dados no SO)
  Network (comunica com outros containers)
  Cache (gerencia as imagens) - Pull, Push
  Daemon API (permite a comunicação com o client)

Registry: (guarda as imagens)
  Images (Cache)