[![Build & Push](https://github.com/kumaxim/wpcli-keep-running/actions/workflows/build-for-docker-hub.yml/badge.svg)](https://github.com/kumaxim/wpcli-keep-running/actions/workflows/build-for-docker-hub.yml)

# WP CLI: Keep Running Containers

Keep running [WP_CLI](https://wp-cli.org/) in Docker container for continuously operation. 

Fork of official Docker [WordPress image][docker-wordpress] by the Docker Community. 

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

#### However, [GitHub Actions][github-ci] won't let you override `CMD` for [service containers][github-sc].
This image was build to get rid of this problem.    


## Solution

Replace values in `CMD` argument in `Dockerfile`(s) by default. That is what this image does. 

## Available tags

All tags from official Docker [WordPress image][docker-wordpress] were preserved. 

If you're previously defined base images as:
```
services:
  wpcli:
    image: wordpress:cli-2.6-php7.4
```

...you just need to replace the name:
```
services:
  wpcli:
    image: kumaxim/wpcli-keep-running:cli-2.6-php7.4
```

Full example of using this image in [GitHub Actions][github-ci] Workflow may be found inside `e2e-tests` job in [this pipeline][pcop1-pipeline]. 

## Copyright

[Maxim Kudryavtsev](https://k-maxim.ru/). 2022. All rights reserved.

The code in this repository distribute under General Public License version 2 or any later.

[wordpress-image]: https://hub.docker.com/_/wordpress
[github-ci]: https://github.com/features/actions
[github-sc]: https://docs.github.com/en/actions/using-containerized-services/about-service-containers
[docker-wordpress]: https://github.com/docker-library/wordpress
[pcop1-pipeline]: https://github.com/kumaxim/pull-comnents-other-pages/blob/master/.github/workflows/build-plugin-release.yml