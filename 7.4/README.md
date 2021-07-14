# PHP7.4 (PHP-FPM)

Build and configure a PHP-FPM (PHP7.4) image from an official [PHP-FPM Alpine Linux build](https://hub.docker.com/_/php/?tab=tags&page=1&ordering=last_updated&name=7.4-fpm-alpine).

## Beware

The project uses the **[docker-php-extension-installer](https://github.com/mlocati/docker-php-extension-installer)** script from [Michele Locati](https://github.com/mlocati).

If you already use the **mlocati/php-extension-installer** image locally, be sure you have the latest version by running :

```sh
docker pull mlocati/php-extension-installer
```

## Configuration

This image ships with the default **php.ini-production** configuration file.

This default config can be customized by editing the [zzz-prod.ini configuration files](7.4/conf.d/zzz-prod.ini) into the [conf.d/](7.4/conf.d/) directory.

## How to use

Run the commands to build and run the Docker image:

```sh
DOCKER_BUILDKIT=1 docker build --no-cache --tag my-php-fpm .

docker run --detach --interactive --tty --rm --name my-running-php-fpm --volume /var/www:/var/www --expose 9000 my-php-fpm
```

## How to install more PHP extensions

Many extensions are already compiled into the image :

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
DOCKER_BUILDKIT=1 docker build --no-cache --build-arg user_extension=gd --tag my-php-fpm .

docker run -dit --rm --name my-running-php-fpm my-php-fpm
```

For example, if you want to have a PHP-FPM image with the **mysqli** and **pdo_mysql** extension, run the commands:

```sh
DOCKER_BUILDKIT=1 docker build --no-cache --build-arg user_extension="mysqli pdo_mysql" --tag my-php-fpm .

docker run -dit --rm --name my-running-php-fpm my-php-fpm
```
