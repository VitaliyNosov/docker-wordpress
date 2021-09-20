# Docker + WordPress
##### Docker: https://www.docker.com/

<img src="https://i.ibb.co/d4vyrRm/docker-bg.png">

__Docker__ allows you to quickly build a set of containers and deploy __WordPress__ development. Then, just as quickly, transfer it all to any system. The "docker-compouse" file is provided, which is a set of instructions for __Docker__ that will download and install all dependencies. You only need to install __Docker__ on your computer.

__command to  start :__

```git 
docker-compose up -d
```

```yaml

version: "3"
services:
  #MySQL Database image
  my_database:
    image: mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: my_password_1234789
      MYSQL_DATABASE: my_wp_database
      MYSQL_USER: my_wp_user
      MYSQL_PASSWORD: my_wp_user_password
    volumes:
      - mysql:/var/lib/mysql

  #WordPress image based on Apache
  wordpress:
    depends_on:
      - my_database
    image: wordpress:latest
    restart: always
    ports:
      - "8000:80"
    environment:
      WORDPRESS_DB_HOST: my_database:3306
      WORDPRESS_DB_USER: my_wp_user
      WORDPRESS_DB_PASSWORD: my_wp_user_password
      WORDPRESS_DB_NAME: my_wp_database
    volumes:
      ["./:/var/www/html"]

  phpmyadmin:
    depends_on:
      - my_database
    image: phpmyadmin/phpmyadmin
    restart: always
    ports:
      - '8080:80'
    environment:
      PMA_HOST: my_database
      MYSQL_ROOT_PASSWORD: my_password_1234789
      
volumes:
  mysql: {}


```


