↖ _The autogenerated table of contents is here_

# PHP7.4-FPM

Build and configure a PHP-FPM (PHP7.4) image from an official [PHP-FPM Alpine Linux build](https://hub.docker.com/_/php/?tab=tags&page=1&ordering=last_updated&name=7.4-fpm-alpine).

## Requirements

- Docker version ^20.10

## Beware

The project uses the **[docker-php-extension-installer](https://github.com/mlocati/docker-php-extension-installer)** script from [Michele Locati](https://github.com/mlocati).

If you already use the **mlocati/php-extension-installer** image locally, be sure you have the latest version by running :

```sh
docker pull mlocati/php-extension-installer
```

## Configuration

This image will ship with the default **php.ini-production** configuration file.

This default config can be customized by editing the [zzz-prod.ini configuration file](https://github.com/ojullien/php-fpm-dockerfiles/blob/main/7.4/conf.d/zzz-prod.ini) from the [conf.d/](https://github.com/ojullien/php-fpm-dockerfiles/tree/main/7.4/conf.d) directory.

*Note: I use this image for my own projects, the configuration file contains the settings and modules I need. It's completely customizable to your needs.*
*You may find more PHP-FPM configuration and pool templates [in this repository](https://github.com/ojullien/php-fpm)*

## How to use

Run the commands to build and run the Docker image:

```sh
DOCKER_BUILDKIT=1 docker build --no-cache --tag my-php7.4-fpm .

docker run --detach --interactive --tty --rm --name my-running-php7.4-fpm \
           --volume /var/www:/var/www --workdir /var/www \
           --publish 127.0.0.1:9074:9000 \
           my-php7.4-fpm
```

- Default working directory is `/var/www`.
- Default port for the fcgi protocol is `9000`.

## How to install more PHP extensions

Many extensions are already compiled / or will be automatically compiled into the image :

|  |  |  |  |  |  |
|:---:|:---:|:---:|:---:|:---:|:---:|
| ctype | curl |   |   |   |   |
| date | dom |   |   |   |   |
| fileinfo | filter | ftp |   |   |   |
| hash |   |   |   |   |   |
| iconv |   |   |   |   |   |
| json |   |   |   |   |   |
| libxml |   |   |   |   |   |
| mbstring | mysqlnd |   |   |   |   |
| openssl | OPcache |   |   |   |   |
| pcre | PDO | pdo_sqlite | Phar  | posix |   |
| readline | Reflection |   |   |   |   |
| session | SimpleXML | sodium | SPL | sqlite3 | standard |
| tokenizer |   |   |   |   |   |
| xml | xmlreader | xmlwriter |   |   |   |
| zlib |   |   |   |   |   |

And, to easily install more PHP extensions, we provide a variable that you can pass at build-time to the builder with the `docker build` command using the `--build-arg user_extension=<value>` flag.

For example, if you want to have a PHP-FPM image with the **gd** extension, run the commands:

```sh
DOCKER_BUILDKIT=1 docker build --no-cache --build-arg user_extension=gd --tag my-php7.4-fpm .

docker run --detach --interactive --tty --rm --name my-running-php7.4-fpm \
           --volume /var/www:/var/www --workdir /var/www \
           --publish 127.0.0.1:9074:9000 \
           my-php7.4-fpm
```

Another example, if you want to have a PHP-FPM image with the **mysqli** and **pdo_mysql** extensions, run the commands:

```sh
DOCKER_BUILDKIT=1 docker build --no-cache --build-arg user_extension="mysqli pdo_mysql" --tag my-php7.4-fpm .

docker run --detach --interactive --tty --rm --name my-running-php7.4-fpm \
           --volume /var/www:/var/www --workdir /var/www \
           --publish 127.0.0.1:9074:9000 \
           my-php7.4-fpm
```

# Documentation

- [PHP Official image](https://hub.docker.com/_/php/)
- [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)
- [docker build](https://docs.docker.com/engine/reference/commandline/build/)
- [docker run](https://docs.docker.com/engine/reference/commandline/run/)
- [Best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

# Contributing

Thanks you for taking the time to contribute. Please fork the repository and make changes as you'd like.

If you have any ideas, just open an [issue](https://github.com/ojullien/php-fpm-dockerfiles/issues) and tell me what you think. Pull requests are also warmly welcome.

If you encounter any **bugs**, please open an [issue](https://github.com/ojullien/php-fpm-dockerfiles/issues).

Be sure to include a title and clear description,as much relevant information as possible, and a code sample or an executable test case demonstrating the expected behavior that is not occurring.

# License

**PHP-FPM dockerfiles** is open-source and is licensed under the [MIT License](https://github.com/ojullien/php-fpm-dockerfiles/blob/master/LICENSE).
