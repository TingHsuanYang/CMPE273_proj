# CMPE273_proj

## Prerequisites

- We are using [Postman](https://www.postman.com/downloads/) as client.
- We need [Docker](https://www.docker.com/products/docker-desktop) to run the server and DB.  

    Check docker version

    ```shell
    docker --version
    ```

    Create Docker Network - techbankNet

    ```shell
    docker network create --attachable -d bridge techbankNet
    ```

    Install or init [docker compose](https://docs.docker.com/compose/install)

- Run docker compose:

    ```shell
    docker-compose up -d
    ```

- Run MongoDB  

    Download Client Tools – [Robo 3T](https://robomongo.org/download):

    Run in Docker:

    ```shell
    docker run -it -d --name mongo-container \
    -p 27017:27017 --network techbankNet \
    --restart always \
    -v mongodb_data_container:/data/db \
    mongo:latest
    ```

- MySQL

    Run in Docker:

    ```shell
    docker run -it -d --name mysql-container \
    -p 3306:3306 --network techbankNet \
    -e MYSQL_ROOT_PASSWORD=techbankRootPsw \
    --restart always \
    -v mysql_data_container:/var/lib/mysql  \
    mysql:latest
    ```

    Client tools in Docker – Adminer:

    ```shell
    docker run -it -d --name adminer \
    -p 8080:8080 --network techbankNet \
    -e ADMINER_DEFAULT_SERVER=mysql-container \
    --restart always adminer:latest
    ```
