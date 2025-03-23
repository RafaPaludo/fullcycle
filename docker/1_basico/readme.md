## Comandos Básicos do Docker

`docker ps` - mostra containers rodando
`docker ps -a`- mostra containers ativos e inativos
`docker start <ID do container>` - inicia o container
`docker stop <ID do container>` - mata o container
`docker rm <ID do container>` - remove o container do histórico
`docker rm <ID do container> -f` - força a parada do container e remove o container do histórico

## Sintaxe básica Docker run

`docker run <parametros> <nome da imagem> <comando>`
`docker run -it ubuntu bash`
`docker run <nome da imagem:versão da imagem>` - roda um container com a imagem selecionada
`docker run --rm <nome da imagem>`- o --rm não cria histórico da execução do container
`docker run -p 5000:8080 <nome da imagem>` - faz com que o docker mepeie a porta 5000 do host para a porta 8080 do container
`docker run -d <nome da imagem>`- modo detached, não bloqueia o terminal
`docker run --name <nome do container> <ID do container>` - executa um container e define um nome para eles
`docker exec <nome do container> <comando>`- Executa comando dentro de um container que já está em execução.

## Alterando arquivos num container nginx

`docker run --name nginx -d -p 8080:80 nginx" - sobe o container
`docker exec -it nginx bash`- entra no bash do container de modo interativo
`cd /usr/share/nginx/html`- acessa o arquivo html padrão do nginx
`apt-get update` - atualiza o apt-get
`apt-get install vim` - instalar o vim para poder alterar o arquivo
`vim index.html`- abre o arquivo com o vim (i - para editar, esc - para sair, SHIFT + : w - para salvar, SHIFT + :q - para sair)

## Bind mounts
Podemos usar a ideia de volumes para mapear uma pasta / arquivo do computador local para dentro do container, caso o arquivo não exista, ele cria ele localmente. Dessa forma tudo o que for escrito durante a execução do container será salvo no arquivo local e não é perdido ao matar o container.
`docker run -v <caminho pasta local>:<caminho pasta container>`
Ex: `docker run --name nginx -d -p 8080:80 -v "$(pwd)"/html/:/usr/share/nginx/html nginx`

Além de usar o comando -v (Volumes), podemos usar um outro comando mais explícito e moderno, que é o --mount. Nesse formato, não há criação de arquivo como é feito com o -v.
`docker run --mount type=bind,source=<caminho pasta local>,target=<caminho pasta container>`
Ex: `docker run --name nginx -d -p 8080:80 --mount type=bind,source="$(pwd)"/html/,target=/usr/share/nginx/html nginx`

## Trabalhando com Volumes
Esse é cum conceito do próprio docker, que permite criar um volume localmente, e utilizar ele ao inveś de uma pasta específica como é feita com o Bind Mounts acima. Os volumes também permitem compartilhá-los entre diversos containers ao mesmo tempo, sendo mais poderoso do que o bind mounts.
1 - Cria-se um volume:
`docker volume create <nome do volume>`
Ex: `docker volume create meu-volume`

2 - É possível ver onde o volume está:
`docker volume inspect <nome do volume>`
Ex; `docker volume inspect meu-volume`

3 - Faz o mount para dentro do container utilizando o volume:
`docker run -d --mount type=volume,source=<nome do volume>,target=<pasta> <nome da imagem>` OU `docker run -d -v <nome do volume>:<pasta> <nome da imagem>`
ex: `docker run --name nginx -d --mount type=volume,source=meu-volume,target=/app nginx`

4 - Criar novos containers e mapear o mesmo volume:
ex: `docker run --name nginx2 -d --mount type=volume,source=meu-volume,target=/app nginx`
ex: `docker run --name nginx3 -d --mount type=volume,source=meu-volume,target=/app nginx`
ex: `docker run --name nginx4 -d --mount type=volume,source=meu-volume,target=/app nginx`

5 - Criar, remover, editar qualquer arquivo em algum conteiner irá refletir nos demais!