# SuiteCRM
SuiteCRM is popular customer relationship management (CRM) system.

## Docker Environment

You can use a Dockerfile to create Docker image and run SuiteCRM in Docker container.
The following command will help you to run two Docker Containers:
 - Apache2 HTTP Web Server on port 80 inside Docker container;
```sh
docker run --name suitecrm -p 80:80 -d andriykoval/suitecrm:latest
```
 - MariaDB Database Server on port 3306 inside Docker container;
```sh
docker run --name suitecrm_db -e MYSQL_DATABASE='suitecrm' -e MYSQL_USER='suitecrm' -e MYSQL_PASSWORD='SuiteCRM' -e MYSQL_ALLOW_EMPTY_PASSWORD='no' -e MYSQL_ROOT_PASSWORD='mysql' -p 3306:3306 -d mariadb:10.0.34
```

### Docker Compose
You can run whole Docker environment via Docker compose:

```sh
version: '3.4'

services:

  suitecrm:
    build: .
    image: suitecrm:latest
    container_name: suitecrm
    ports:
      - "80:80"

  suitecrm_db:
    image: mariadb:10.0.34
    container_name: suitecrm_db
    restart: always
    environment:
      - MYSQL_DATABASE=suitecrm
      - MYSQL_USER=suitecrm
      - MYSQL_PASSWORD=SuiteCRM
      - MYSQL_ALLOW_EMPTY_PASSWORD=no
      - MYSQL_ROOT_PASSWORD=mysql
    ports:
      - "3306:3306"
```
