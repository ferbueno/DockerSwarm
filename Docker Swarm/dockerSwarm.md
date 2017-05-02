# Docker Swarm

Docker Swarm es la aproximación para Cluster Management de Docker, la cual se basa en nodos maestros y nodos trabajadores. Los nodos maestros (o managers) tienen asignan trabajo a los nodos trabajadores y a ellos mismos, además de tener la jerarquía necesaria para realizar operaciones en el swarm.

### Inicialización de Swarm

 **docker swarm init**

    _docker swarm init_ inicializa un Docker Swarm, con el nodo maestro por default en el sistema donde fue creado. La respuesta de este comando será _docker swarm join_ a la par de un token, para que otro nodo pueda unirse al swarm.

    ```
	 $ sudo docker swarm init
	```

### Unirse a un Swarm
 
 **docker swarm join [TOKEN] [HOST]**
 
   _docker swarm join_ permite a un nuevo sistema unirse a un Swarm; esta función requiere de un argumento, el cual es el token generado al inicializar el Swarm.

   ``` 
  	  $ sudo docker swarm join \
  	     --token SWMTKN-1-51xcg7anx0in93l9363p00b2bokto41slp57hzckgx8qaebfdw-8yirvjqcprnr1qb7wi7f4onjj \
  	     172.22.40.131:2377
   ```

 ### Imágenes

	    En Docker Swarm los contenedores y servicios se rigen por imágenes, que tanto pueden estar guardadas en el repositorio de Docker (librería Docker), en un repositorio local creado por el Swarm, o en un repositorio propio de Docker.

	  #### Tags

	    Una imagen tiene asociada un _tag_, que normalmente se refiere a la versión de la imagen. Al manipular imágenes sin tag, por default se establece el tag _latest_.

	  #### Digests

	    El _digest_ es un hash asignado a una imagen que tiene un tag y pertenece a un repositorio, es necesario que una imagen tenga un digest asignado para que se pueda asignar a servicios.

	  #### Descarga de imágenes

	    **docker pull <IMAGE>:<TAG>**

	    Para descargar una imagen solo se utiliza _docker pull_. El tag es opcional.

	    ``` 
	      	$ sudo docker pull nginx
	    ``` 
	  #### Compilación de imágenes

	    **docker build -f <PATH TO DOCKERFILE> .**

	      Para crear una imagen propia, es necesario compilarla a través de un Dockerfile. Con la instrucción _build_ podemos compilar una imagen para agregarla a un repositorio propio.

	      ``` 
	      	 $ sudo docker build -f /code/findmark/release/docker/Dockerfile .
	      ``` 
	  #### Tag de imágenes

	    **docker tag <IMAGE ID> <TAG>**

	       Para que docker sea capaz de identificar y cargar una imagen creada, es necesario agregarles un _tag_.

	       ``` 
	      	 $ sudo docker tag 8b64173df4d4 ferbueno/nginx
	      ```

	  #### Carga de imágenes al repositorio

	    **docker push <IMAGE>

	       Una vez que se haya realizado el _tag_ de la imagen, se puede cargar a un repositorio. **Es importante** mencionar que para Docker Swarm este es un proceso necesario, para que todos los nodos puedan acceder a la misma imagen.

	       	``` 
	      	 $ sudo docker push ferbueno/nginx
	        ```

	  #### Lista de imágenes descargdas

	    **docker image ls**

	    	Para conocer cuántas imágenes tiene disponible cada nodo.

	    	``` 
	      	 $ sudo docker image ls
            ```
      #### Eliminar imagen

        **docker rmi <IMAGE>**

        	Si hay que eliminar una imagen para que vuelva a ser descargada, o ya no es necesaria. Si la imagen es utilizada por uno o más contenedores, se deben detener los contenedores primero.

        	``` 
	      	 $ sudo docker rmi ferbueno/nginx
            ```

 ### Servicios

 	Los servicios correrán interpretarán las tareas que deben realizarse. Un servicio se puede replicar para correr en varios contenedores encargados de correr la tarea asignada por el servicio. Se pueden replicar y escalar lor servicios.

    #### Crear un servicio

      **docker service create _OPTIONS_ <IMAGE>**

      Crea un servicio basándose en la imagen que se manda como parámetro.

      ``` 
	       $ sudo docker create --name nginxService ferbueno/nginx
      ```

    #### Enlistar un servicio

      **docker service ls**

      Enlista todos los servicios activos.

       ``` 
	       $ sudo docker service ls
      ```

    #### Detalles de un servicio

      **docker service ps <SERVICE>**

      Muestra los detalles del estado servicio específico elegido sobre el swarm.

       ``` 
	       $ sudo docker service ps nginx
      ```

    #### Inspeccionar un servicio

      **docker service inspect <SERVICE>**

      Muestra a detalle el servicio.

      ``` 
	       $ sudo docker service inspect --pretty nginxService
      ```

      _Para una inspección más profunda, es necesario quitar la bandera '--pretty'_

    #### Eliminar un servicio

      **docker service rm <SERVICE>**

      Elimina el servicio especificado de la lista de servicios.

 ### Contenedores

     Los contenedores correrán las tareas que el servicio les asigne. Se creará un contenedor por cada réplica de cada servicio que exista.


     #### Enlistar los contenedores

     **docker container ls**

     Muestra la lista de los contenedores corriendo en el nodo del Swarm.

      ``` 
	       $ sudo docker container ls
      ```

     Muestra la lista de todos los contenedores del Swarm.

      ``` 
	       $ sudo docker container ls -a
      ```

     #### Inspeccionar los contenedores

     **docker container inspect <CONTAINER ID>

     Es posible inspeccionar los detalles de cada contenedor, aquí se pueden ver los detalles como la dirección IP del contenedor.

      ``` 
	       $ sudo docker container inspect 
      ```
     #### Obtener los logs del contenedor

     **docker container logs <CONTAINER ID>**

     Cuando se necesita saber que ocurre dentro del contenedor, es posible ver los logs del mismo, para verificar que los procesos de terminal se ejecuten de manera correcta.

      ``` 
	       $ sudo docker container logs  80645a00ccff
      ```   

     #### Correr instrucciones de terminal en un contenedor

     **docker container exec <CONTAINER ID> <BASH COMMAND>** 

     De ser necesario, es posible correr comandos de terminal sobre un contenedor específico, para probar diferentes aspectos del mismo, del servicio o de la imagen que está corriendo dentro.

      ``` 
	       $ sudo docker container exec  80645a00ccff echo "Hello World!"
      ```

