Date:2015-10-08 19:33
Title:Initialize Wordpress with Docker Compose
Author:Lotp
tags:Wordpress, Docker, Docker Compose

Previously, I' ve talked about the initialization of wordpress with docker on this [post][lastOne]

Today I'm gonna introduce a more robust way to do this.

[lastOne]:initialize-wordpress-with-docker.html

###Preparations
1.	Ensure you had *docker* and *docker-compose* installed on your machine.
1.	Create an directory where you could save related files, lets call it tem.
1.	Create another directory within tem called content
###Create 3 files in tem
*	docker-compose.yml
```yaml
db:
        build: .
        dockerfile: wordpressDb.dockerfile
        container_name: DB
server:
        build: .
        dockerfile: wordpress.dockerfile
        container_name: Server
        ports:
             - "your ip address:50003:80"
        volumes:
             - ./content:/var/www/html                         
        links:
             - db:mysql
```
*	wordpress.dockerfile
```yaml
FROM wordpress
ENV MYSQL_ROOT_PASSWORD=password
```

*	wordpressDb.dockerfile
```yaml
FROM mysql:5.7
ENV MYSQL_ROOT_PASSWORD=password
ENV MYSQL_DATABASE=wordpress
```
###	Create your wordpress dev site
1.	Open a terminal and `cd` to tem.
1.	Run `docker-compose up`.
1.	Open your browser, go to **your ip address:50003**.
1.	Enjoy your new wordpress blog.
