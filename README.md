[![Build and Publish Images on Docker Hub](https://github.com/kumaxim/wpcli-keep-running/actions/workflows/.docker-hub.yml/badge.svg)](https://github.com/kumaxim/wpcli-keep-running/actions/workflows/.docker-hub.yml)

# WP CLI: Keep Running Containers

Keep running [WP_CLI](https://wp-cli.org/) in Docker container for continuously operation.

## Quick Start

Image on Docker Hub: [kumaxim/wpcli-keep-running](https://hub.docker.com/r/kumaxim/wpcli-keep-running)

Using in terminal:

`docker run --rm --name wpcli-running kumaxim/wpcli-keep-running:cli-2.6-php7.4`

Using within `docker-compose.yml`

```
version '3.1'

services:
  wpcli:
    image: kumaxim/wpcli-keep-running:cli-2.6-php7.4
```  

## Problem
Container based on Docker's official `wordpress:cli` image will exit after successfully finished `wp` command. 
This is because `CMD` line in official `Dockerfile` looks like: `CMD ['wp', 'shell']`. The common workaround that allow preventing
stopping container is re-define `CMD` option while starting container:

_docker-compose.yml_
```
version '3.1'

services:
  wpcli:
    image: wordpress:cli
    command: ['tail', '-f', '/dev/null']
```   

...or in terminal: 

```docker run --rm --name wpcli wordpress:cli tail -f /dev/null```


## Solution

Replace values in `CMD` argument in `Dockerfile`(s) by default. That is what this image do. 

## Tag mapping

Not all tags/labels was added from original image to this yet. See relationships in the table bellow.

| Docker's tag | This image |
| ------------| :---------: |
| cli-2.6.0        | cli-2.6-php7.4 |
| cli-2.6          | cli-2.6-php7.4 |
| cli-2            | cli-2.6-php7.4 |
| cli              | cli-2.6-php7.4 |
| cli-2.6.0-php7.4 | cli-2.6-php7.4 |
| cli-2.6-php7.4   | cli-2.6-php7.4 |
| cli-2-php7.4     | cli-2.6-php7.4 |
| cli-php7.4       | cli-2.6-php7.4 |
| cli-2.6.0-php8.0 | cli-2.6-php8.0 |
| cli-2.6-php8.0   | cli-2.6-php8.0 |
| cli-2-php8.0     | cli-2.6-php8.0 |
| cli-php8.0       | cli-2.6-php8.0 |
| cli-2.6.0-php8.1 | cli-2.6-php8.1 | 
| cli-2.6-php8.1   | cli-2.6-php8.1 |
| cli-2-php8.1     | cli-2.6-php8.1 |
| cli-php8.1       | cli-2.6-php8.1 |


## Credits

Based on Docker's [Official WordPress Images](https://hub.docker.com/_/wordpress)

## Others

Maintainer: [Maxim Kudryavtsev](https://k-maxim.ru/)

Issues: [Github](https://github.com/kumaxim/wpcli-keep-running/issues)