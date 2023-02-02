###you can go to site ```bash 
https://www.composerize.com/``` then you can maker multiple container
##I create docker compose file with extension .yml
```bash
#version of docker_compose file you perfer to make ultimate version
version: "3"
#containers
services:
#db layer for wp >> MYSQL DB
 mysql_database:
   #caracteristique of my container
   image: mysql
   #restart if container down
   restart: always
   #env_vaar(pwd,user..)
   environment:
     #admin
     MYSQL_ROOT_PASSWORD: 123456
     MYSQL_DATABASE: wp_db
     MYSQL_USER: wp_user
     #user no admin
     MYSQL_PASSWORD: 123456
     #persit data
   volumes:
     #in_my_host:in_container
     - mysql:/var/lib/mysql
 #wp layer (by default wp work on apache ==> apache port 80)
 wordpress:
  #start this container if MYSQL running
   depends_on:
     - mysql_database
   image: wordpress:latest
   restart: always
   ports:
     - "8080:80"
   #db to connect on
   environment:
     WORDPRESS_DB_HOST: mysql_database:3306
     WORDPRESS_DB_USER: wp_user
     WORDPRESS_DB_PASSWORD: 123456
     WORDPRESS_DB_DB: wp_db
   volumes:
     ["./var/www/html"]
  #image for phpmyadmin to visualize my db
 phpmyadmin:
   depends_on:
     - mysql_database
   image: phpmyadmin/phpmyadmin
   restart: always
   ports: 
     - "8000:80"
   environment:
     PWA_HOST: mysql_database
     MYSQL_ROOT_PASSWORD: 123456
#top evel volumes
volumes:
  mysql: {}


```

###after that u can check you yml file by going to site 
```bash
https://www.yamllint.com/
``` 
### proprietaire dossier docker
```bash
sudo chown $USER /var/run/docker.sock
```

###then we tipe command
```bash
docker-compose up -d
```
### we can create in CLI 
```bash
sensible-browser http://127.0.0.1:8080
```
or go to browser and create the URI

### for check container and network 
```bash
docker container ls
```
```bash
docker network ls
```
### for show more details for network
```bash
docker network inspect wordpresscompose_default
```
### for delete all container
```bash
docker compose down
```

    
    
   
   

   
   

