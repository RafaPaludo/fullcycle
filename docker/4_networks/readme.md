## Tipos de Network (drivers)
- bridge: network padrão
- host: mescla a network com o Docker Host, ou seja, com a rede local. Permite o container acessar portas locais sem necessidade de expor as portas manualmente
- overlay: permite vários containers se comuniquem de forma clusterizada entre si
- maclan: usa mac address, pouco usado 
- none: nenhuma rede, forma isolada

## Comandos Network
`docker network` - lista os comandos de rede
`docker network inspect bridge`- mostra informações sobre a rede bridge, principalmente sobre quais containers estão utilizando ela
`docker network create --driver <tipo driver> <nome da rede>` - Cria uma nova rede com o tipo escolhido
ex: docker network create driver --bridge minha-rede
`docker network connect <nome da rede> <nome do container>` - Conecta um container a uma rede
ex: docker network connect minha-rede nginx
`docker network disconnect <nome da rede> <nome do container>` - Desconecta um container de uma rede
ex: docker network disconnect minha-rede nginx
`docker network rm <nome da rede>` - Remove uma rede
ex: docker network rm minha-rede