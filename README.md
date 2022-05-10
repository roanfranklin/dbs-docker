## Docker Databases

Caso precise, aqui estão alguns do SGDB para uso local (desenvolvimento e testes).


### Pré-requisitos

- docker
- docker-compose

### Configuração inicial

Primeiramente crie os diretórios onde ficarão os dados de cada SGDB caso inicie com o YML abaixo.

```bash
mkdir -p data/{MySQL,PostgresSQL,MongoDB,SQLServer2019}
```

### Arquivo docker-compose.yml

No arquivo abaixo estão alguns do SGDBs e então vocẽ pode levantar todos, ou então personalizar para levantar o que deseja testa-lo.

```yaml
version: '3'

services:
   mysql:
     image: mysql:5.7
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: 'MySQL2022!'
       MYSQL_DATABASE: 'wordpress'
       MYSQL_USER: 'wordpress'
       MYSQL_PASSWORD: 'wordpress'
     ports:
      - 3306:3006
    volumes:
       - data/MySQL:/var/lib/mysql

  postgres:
    image: postgres
    restart: always
    environment:
      POSTGRES_PASSWORD: 'PostgresSQL!'
    ports:
      - '5432:5432'
    volumes:
      - data/PostgreSQL:/var/lib/postgresql/data

  mongo:
    image: mongo
    restart: always
    environment:
      MONGO_INITDB_ROOT_USERNAME: 'root'
      MONGO_INITDB_ROOT_PASSWORD: 'MongoDB2022!'
    ports:
      - '27017:27017'
    volumes:
      - data/MongoDB:/data/db

  sql2019:
    image: mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
    environment:
      ACCEPT_EULA: Y
      SA_PASSWORD: 'SqlServer2022!'
    ports:
      - '1433:1433'
    volumes:
      - data/SQLServer2019:/var/opt/mssql
```

### Comandos docker-compose

```bash
docker-compose up -d
docker-compose down

docker-compose start
docker-compose stop

docker-compose logs -f
```