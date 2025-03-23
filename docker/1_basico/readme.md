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