# This is just docker-compose for development environment

### Services

- Database
- Observer tool



### Dockerfile

Dockerfile to build image for php application with nginx, php-fpm with supervisor

- COPY any file to `"$PHP_INI_DIR/conf.d"` directory for php config
- COPY any supervisor to `/etc/supervisor/conf.d` directory for process like queue:work
