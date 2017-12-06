# Supported tags and respective `Dockerfile` links

-	[`latest`, `php7.1` (*php7.1/fpm/Dockerfile*)](https://github.com/mybb/docker-compose/blob/master/php7.1/fpm/Dockerfile)
-	[`php7.2` (*php7.2/fpm/Dockerfile*)](https://github.com/mybb/docker-compose/blob/master/php7.2/fpm/Dockerfile)
-	[`php5.6` (*php5.6/fpm/Dockerfile*)](https://github.com/mybb/docker-compose/blob/master/php5.6/fpm/Dockerfile)

# Quick reference

-	**Where to get help**:  
	[the MyBB Community Forums](https://community.mybb.com/)

-	**Where to file issues**:  
	[https://github.com/mybb/docker-compose/issues](https://github.com/mybb/docker-compose/issues)

-	**Maintained by**:  
	[the MyBB Team](https://mybb.com/about/team/)

# What is MyBB?

MyBB is the free and open source, intuitive, extensible, and incredibly powerful forum software you've been looking for. With everything from forums to threads, posts to private messages, search to profiles, and reputation to warnings, MyBB features everything you need to run an efficient and captivating community. Through plugins and themes, you can extend MyBB's functionality to build your community exactly as you'd like it. Learn more at [MyBB.com](https://mybb.com).

> [wikipedia.org/wiki/MyBB](https://en.wikipedia.org/wiki/MyBB)

![logo](https://mybb.com/assets/images/logo.png)

# How to use this image

```console
$ docker run mybb/mybb:latest
```

This image only provides a MyBB service container running PHP7.X-FPM. There are no database or nginx container(s) provided, you'll need to use Docker Compose or Stack to wrange those additional services to your MyBB instance. Please see the provided mysqli/pgsql Compose example files in the official repository, [here](https://github.com/mybb/docker-compose). A very basic example has also been provided below.

## ... via [`docker stack deploy`](https://docs.docker.com/engine/reference/commandline/stack_deploy/) or [`docker-compose`](https://github.com/docker/compose)

Example `stack.yml` for `mybb`:

```yaml
version: '3.4'
services:
  nginx:
    image: nginx:mainline
    ports:
      - '8080:80'
    volumes:
      - ${PWD}/mybb:/var/www/html:ro

  mybb:
    image: mybb/mybb:latest
    volumes:
      - ${PWD}/mybb:/var/www/html

  postgresql:
    image: postgres:10.1
    environment:
      POSTGRES_DB: mybb
      POSTGRES_USER: mybb
      POSTGRES_PASSWORD: changeme
    volumes:
      - ${PWD}/postgres/data:/var/lib/postgresql/data
```
