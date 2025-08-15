# This is just docker-compose for development environment

## Usage

Copy env
`cp .env.exmpale to .env`

run container
`docker-compose up`

### Services

- Database
- Observer tool

### Dockerfile

Dockerfile to build image for php application with nginx, php-fpm with supervisor

- COPY any file to `"$PHP_INI_DIR/conf.d"` directory for php config
- COPY any supervisor to `/etc/supervisor/conf.d` directory for process like queue:work

### Elastic, Kibana, Filebeat

#### Kibana

```sh


docker exec -it kibana /usr/bin/bash

# run in elastic instance
./bin/elasticsearch-reset-password -i -u kibana_system

./bin/kibana-keystore create

./bin/kibana-keystore add elasticsearch.password
```