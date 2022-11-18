# docker-compose-wordpress4sd
docker compose wordpress4sd sube una imagen de mysql:5.7 con la ultima vesion de wordpress, se usa docker-compose v:2.5

se debe tener docker y docker-compose instalados en la maquina para poder subir los contenedores

referencia practica, muy buena:
https://www.youtube.com/watch?v=yvntTvrBgiQ
ejm video:
docker-compose.yml: se debe tener especial cuidado con la identacion

comandos docker compose
===========================
docker-compose --version      --> nos dice la version, ejm: Docker Compose version v2.5.0
docker compose up             --> sube el archivo docker-compose.yml, con la configuracion definido en el mismo, abraza la consola
docker-compose up -d          --> sube el archivo docker-compose.yml, con la configuracion definido en el mismo, NO abraza la consola, modo silencioso
docker compose down           --> baja los contenedores que estan arriba, pero persiste los volumenes o disco definido para los contenedores
docker-compose down --volumes --> baja los contenedores que estan arriba, al igual que los volumenes, apaga todo


version: '2.5.0'
services:
  db:
    image: mysql:5.7
    volumes:
     - db_data:/var/lib/mysql
    restart: always
    environment:
     MYSQL_ROOT_PASSWORD: wordpress
     MYSQL_DATABASE: wordpress
     MYSQL_USER: wordpress
     MYSQL_PASSWORD: wordpress

  wordpress:
   depends_on:
    - db
   image: wordpress:latest
   ports:
    - "80:80"
   restart: always
   environment:
    WORDPRESS_DB_HOST: db:3306 
    WORDPRESS_DB_USER: wordpress
    WORDPRESS_DB_PASSWORD: wordpress
    WORDPRESS_DB_NAME: wordpress
volumes:
   db_data: {}

