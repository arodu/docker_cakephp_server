# Docker CakePHP Server


## `docker-compose.yml` example

```yml
version: "3"
services:
  project-mysql:
    image: mysql:5.7
    container_name: project-mysql
    working_dir: /application
    command: mysqld --sql-mode='NO_ENGINE_SUBSTITUTION' --character-set-server=utf8 --init-connect='SET NAMES UTF8;'
    environment:
      - MYSQL_USER=my_app
      - MYSQL_PASSWORD=secret
      - MYSQL_ROOT_PASSWORD=password
    volumes:
      - ./project:/application
      - ./tmp/mysql-data:/var/lib/mysql
      #- ./docker/entrypoint:/docker-entrypoint-initdb.d
    ports:
      - "3316:3306"

  project:
    image: arodu/cakephp:nginx-php80-alpine
    working_dir: /application
    container_name: project
    volumes:
      - ./project:/application
      - ~/.ssh:/home/application/.ssh:ro
    ports:
      - "8081:80"
    environment:
      WEB_DOCUMENT_ROOT: /application/webroot
      DATABASE_URL: mysql://root:password@project-mysql:3306/project
      DATABASE_TEST_URL: mysql://root:password@project-mysql:3306/project_test
```