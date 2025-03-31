## Docker Hub
- É o repositório do docker, onde ficam as imagens que baixamos ao tentar criar um container
- As imagens possuem diversas versões
- Normalmente em ambiente de dev, usamos a versão latest e a versão fixa que vamos utilizar
- Podemos apenas baixar a imagem com `docker pull <nome da imagem>`
- Para listar imagens `docker images`
- Para remover imagems `docker rmi <nome da imagem>`

## Criaando uma imagem no Docker
Devemos criar um arquivo Dockerfile, que será a receita de como a imagem deve ser, para criar imagens no Docker. Essa imagem normalmente não será pura, mas sim terá outra imagem de base, por exemplo sendo um ubuntu, nginx, php, etc...

// Dockerfile ::
FROM nginx:latest

RUN apt-get update
RUN apt-get install vim -y
//::

Após criado o Dockerfile, podemos fazer o build da imagem:
`docker build -t <nome da imagem> <caminha até a pasta>`
Ex: docker build -t rafapaludo/nginx-com-vim:latest .

## Mais comandos no Dockerfile
- ` WORKDIR <nome da pasta>` - cria uma pasta dentro do container, e ela será a entrada padrão ao acessar o container.
- `COPY <pasta local> <pasta container>` - copia um arquivo ou pasta do computador para dentro do container

// Dockerfile ::
FROM nginx:latest

WORKDIR /app

RUN apt-get update && \
    apt-get install vim -y

COPY html/ /usr/share/nginx/html/
//::

## CMD
- CMD ["echo", "Hello World!] - o comando CMD executa algo no container assim que ele é criado. Porém caso a pessoa que executa a imagem adicionar outros parâmetros na hora de rodar o docker run ... <parametros novos>, o CMD será substituido pelos novos comandos.

## ENTRYPOINT
- ENTRYPOINT ["echo", "Hello World!] - executa algo assim que o container é criado. Porém diferente do CMD, aqui esse valor não é alterado quando o usuário adicionar novos parâmetros, mas sim irá utilizar esses novos parâmetros para concatenar com o comando do ENTRYPOINT

## Publicar no Docker Hub
`docker push <nome da imagem>`
ex: `docker push rafapaludo/nginx-com-vim:latest`