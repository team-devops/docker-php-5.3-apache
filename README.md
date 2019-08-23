# PHP 5.3 Apache

PHP 5.3 [reached EOL](http://php.net/eol.php) on 14 Aug 2014 and thus, official docker support was [dropped](https://github.com/docker-library/php/pull/20). This will allow you to run your app in PHP 5.3. But please don't use this in production.

# How to use this image.

## With Command Line

For PHP projects run through the command line interface (CLI), you can do the following.

### Build and publish the image

This requires a Docker Hub account.

    docker build -t <your-docker-hub-username>/php5.3-apache .
	docker push <your-docker-hub-username>/php5.3-apache

### Create a `Dockerfile` in your PHP project

    FROM <your-docker-hub-username>/php5.3-apache
    COPY . /usr/src/myapp
    WORKDIR /usr/src/myapp
    CMD [ "php", "./your-script.php" ]

Then, run the commands to build and run the Docker image:

    docker build -t my-php-app .
    docker run -it --rm --name my-running-app my-php-app

### Run a single PHP script

For many simple, single file projects, you may find it inconvenient to write a complete `Dockerfile`. In such cases, you can run a PHP script by using the PHP Docker image directly:

    docker run -it --rm --name my-running-script -v "$PWD":/usr/src/myapp -w /usr/src/myapp <your-docker-hub-username>/php5.3-apache php your-script.php

### Installing modules

To install additional modules use a `Dockerfile` like this:

``` Dockerfile
FROM <your-docker-hub-username>/php5.3-apache

# Installs curl
RUN docker-php-ext-install curl
```

Then build the image:

``` bash
$ docker build -t my-php .
```

### Without a `Dockerfile`

If you don't want to include a `Dockerfile` in your project, it is sufficient to do the following:

    docker run -it --rm --name my-php-app -v "$PWD":/var/www/html <your-docker-hub-username>/php5.3-apache

## Credits

A big credit to [cristianorsolin](https://github.com/cristianorsolin) for creating the original version of this and [helderco](https://github.com/helderco/docker-php-5.3) for the `fpm` version.
of this image.

# License

View [license information](http://php.net/license/) for the software contained in this image.
