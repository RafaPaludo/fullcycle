## Processo Multi Step

Utilizando esse processo, é possível criar uma imagem que tenha vários passos, onde cada etapa gera um produto que será utilizado para o próximo passo para gerar a imagem final.

Como exemplo, teremos a imagem do laravel que terá como nome de builder.
Logo abaixo é usado uma imagem base alphine para gerar a imagem final. Para isso ela recebe os arquivos do laravel que foram baixados na etapa de builder.

## NGINX como proxy reverso

Utilizar o Nginx como proxy reverso é uma boa opção para adicionar segurança na rede.
A ideia aqui é ter o container do Laravel e criar um container do Nginx configurado para acessar o container do laravel na mesma rede.
Para isso precisamos criar uma imagem do nginx que possa acessar o laravel.