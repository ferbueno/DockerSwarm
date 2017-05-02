# Pasos para crear un Swarm y desplegar servicios

 ### 1. Iniciar el Swarm
 ```
 $ sudo docker swarm init
 ```
 ### 2. Unir nodos al Swarm
 ```sh
 $ sudo docker swarm join \
  	--token SWMTKN-1-51xcg7anx0in93l9363p00b2bokto41slp57hzckgx8qaebfdw-8yirvjqcprnr1qb7wi7f4onjj \
  	172.22.40.131:2377
 ```
 ### 3. Construir las imágenes de los servicios
 ``` 
 $ sudo docker build -f /code/findmark/release/docker/Dockerfile .
 ```
 ### 4. Asignar un tag a cada imagen

 _De preferencia un tag para cargarla a un repositorio personal._

 ``` 
 $ sudo docker tag 8b64173df4d4 ferbueno/nginx
 ```
 ### 5. Cargar la imagen al repositorio
 ``` 
 $ sudo docker push ferbueno/nginx
 ```
 ### 6. Crear el archivo docker-compose.yml

 Para consultar un ejemplo, da click [aquí](docker-compose/docker-compose.yml)

 ### 7. Compilar la pila desde el archivo YAML

 ```
 $ sudo docker stack deploy --with-registry-auth -c docker-compose.yml findmark
 ```
 
 ### 8. Verificar que todo esté funcionando
 ```
 $ sudo docker service ls
 ```
