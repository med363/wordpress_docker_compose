![image](https://user-images.githubusercontent.com/56481634/217915071-20868731-36a7-436a-8b34-563e495219f1.png)
### docker-compose.yml
```bash
version: '3.4'
services:
  web:
    image: nginx
    deploy:
    #on a deux modes dans le docker swarm replicated / global
       mode: replicated
       # definir des label a notre ressource
       labels: [WAB_app]
       replicas: 2
          placement:
             constraints: [node.role == manager ]
       #mise a jour
       update_config:
          parallelisme: 2
          delay: 10s
          order: stop-first
       restart_policy:
          condition: on-failure
```
###[[  installer docker-compose sur votre cluster[[un seul point d'entre c'est le master]] swarm
### sur le master]]
### deploy nginx en preciser le fichier el le nom de mon stack
```bash
docker stack deploy -c docker-compose.yml  web
```
### verifier que l'application fonctionne
```bash
docker service ls
```
```bash
docker stack ps web
```
       
