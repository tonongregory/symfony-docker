# A simple Docker for Symfony app

This is a simple docker env to start a new symfony application dev.

- Php 8
- Symfony CLI
- Mysql / Postgres
- Make to help you

## Installation

Requires docker & docker compose
You need first to edit .docker/.env file to name your project, and choose version of php to use.
```
# .docker/.env default values
COMPOSE_PROJECT_NAME=my_awesome_project
UID=1000
GID=1000
PHP_VERSION=8.3
XDEBUG_VERSION=3.3.1
XDEBUG_CONFIG="client_host=host.docker.internal client_port=9000 idekey=PHPSTORM log_level=0"
DOCKER_HTTP_PORT=8080
```

Then copy/past the desired symfony skeleton composer.json from https://github.com/symfony/skeleton at root of the project
You will have the following tree-structure
```
├── composer.json
├── .docker
│   ├── docker-compose.override.yml.dist
│   ├── docker-compose.yml
│   ├── .env
│   ├── .gitignore
│   └── php
│       ├── Dockerfile
│       ├── entrypoint.sh
│       └── ini
│           └── symfony.ini
└── Makefile
```

Then you can run
```
make up
```

Your symfony project will be automatically served by symfony-cli and listening your  DOCKER_HTTP_PORT defined into .docker/.env
You can open on your favorite browser https://localhost:${DOCKER_HTTP_PORT}

You can connect to php container by using
```
make bash
```

## Makefile
```
src/vendor: #[Composer] install dependencies
upd: #[Docker] Start containers detached
up: #[Docker] Start containers
stop: #[Docker] Down containers
down: #[Docker] Down containers
build: #[Docker] Build containers
ps: # [Docker] Show running containers
bash: #[Docker] Connect to php container
logs: #[Docker] Show logs
doctrine/migrations: #[Symfony] Run database migration
cache/clean: #[Symfony] Clean cache
xdebug/on: #[Docker] Enable xdebug
xdebug/off: #[Docker] Disable xdebug
```
