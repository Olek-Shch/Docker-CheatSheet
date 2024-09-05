# Docker Examples
---
**Mysql + PhpMyAdmin:**
  
1 - Mysql
```properties
docker run --name my-mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=exampledb -e MYSQL_USER=user -e MYSQL_PASSWORD=password -p 3306:3306 -d mysql:5.7
```

2 - PhpMyAdmin
```properties
docker run --name my-phpmyadmin -d --link my-mysql:db -p 8080:80 phpmyadmin/phpmyadmin
```
---
**Full PHP Codespace:**
```yaml
version: '3.8'
services:
  php:
    image: php:8.0-apache
    volumes:
      - ./src:/var/www/html
    ports:
      - "8080:80"

  mysql:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: exampledb
      MYSQL_USER: user
      MYSQL_PASSWORD: password
    ports:
      - "3306:3306"

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    environment:
      PMA_HOST: mysql
      MYSQL_ROOT_PASSWORD: root
    ports:
      - "8081:80"
```

To Run: ```docker-compose up```
