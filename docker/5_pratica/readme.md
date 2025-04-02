## Laravel
Nesse momento, iremos criar um Dockerfile a partir do php versão 7.4 para rodar o Laravel versão 9x.
Antes de criar o Dockerfile em si, o ideal é primeiro baixar a imagem do FROM, subir um container de teste e rodar os comandos para saber o que será necessário baixar para fazer as coisas funcionarem.
Nesse caso foi baixado uma imagem do php:7.4-cli, acessada a pasta /var/www (WORKDIR /var/www) que é onde o laravel será instalado e então executado os seguintes passos para poder rodar o laravel:

apt-get update &&
apt-get install libzip-dev -y &&
docker-php-ext-install zip

php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" &&
php composer-setup.php &&
php -r "unlink('composer-setup.php');"
php composer.phar create-project --prefer-dist laravel/laravel laravel

Como o Laravel roda o servidor ao executar `php laravel/artisan serve`, deve ser criado um entrypoint para rodar esse comando:

ENTRYPOINT ["php", "laravel/artisan", "serve"]

O Dockerfile ficou assim:

// Dockerfile ::
FROM php:7.2-cli

WORKDIR /var/www

RUN apt-get update && \
    apt-get install libzip-dev -y && \
    docker-php-ext-install zip

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');"
    
RUN php composer.phar create-project --prefer-dist laravel/laravel laravel

ENTRYPOINT ["php", "laravel/artisan", "serve"]

CMD ["--host=0.0.0.0"]

// ::

// https://laravel.com/docs/9.x/installation
// https://hub.docker.com/_/php/tags?name=7.4



## Node

É possível, a partir de uma imagem, desenvolver alguma aplicação mesmo sem ter o ambiente de desenvolvimento instalado.
Nesse caso a ideia foi executar uma imagem node:15 e fazer o bind de uma pasta específica localmente, dessa forma criamos uma aplicação no ambiente local e usamos o container + bind port + bind volume para executar a aplicação de fato no container.

`docker run --rm -it -v $(pwd)/:/usr/src/app -p 3000:3000 node:15 bash`
`cd /usr/src/app`
`npm init -y`
`npm i express@4.21.2 --save-dev`
`touch index.js`
criar o index.js no pc local
`node index.js` - dentro do container