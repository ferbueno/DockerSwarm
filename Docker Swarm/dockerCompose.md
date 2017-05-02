# Docker Compose
 En Docker Swarm, puede volverse fastidioso desplegar servicio por servicio hasta lograr que todos los servicios que deseemos estén corriendo y funcionando. Por suerte, es posible generar todos los servicios relacionados (de manera arbitraria) en un solo comando; mismo que encargará al nodo maestro repartir los servicios en los nodos disponibles del Swarm. Basándose en un archivo de configuración _YAML_, **docker stack deploy** permite a los desarrolladores crear una pila de servicios relacionados.

 Para entender mejor cómo funciona Docker Compose, hay que repasar un poco sobre las pilas en Docker.

 ## Docker Stack

 Las pilas en Docker Swarm permiten a los desarrolladores manipular un conjunto de servicios como si fueran uno solo, a través de los comandos de pilas. Entre estas operaciones se encuentran el crear, desplegar, inspeccionar y eliminar las mismas.

  ### Desplegar una pila a Swarm

  **docker stack deploy [OPTIONS] STACK**

  A través de esta operación, un desarrollador puede desplegar una pila a Swarm. Para establecer los servicios que el desarrollador requiere en esa pila, es necesario componer un archivo _.yml_, que traerá consigo las especificaciones de los servicios a desplegar. Más sobre eso abajo.

  ```
  $ sudo docker stack deploy -c docker-compose.yml helloWorld
  ```

  ### Listar las pilas

  **docker stack ls**
 
  Con esto se puede ver la lista de todas las pilas que tiene Docker Swarm corriendo.

  ```
  $ sudo docker stack ls
  ```
  ### Listar los servicios de las pilas

  **docker stack services**

  Si un desarrollador quisiera ver los servicios que fueron desplegados con la pila, debe usar esta instrucción. 

  ```
  $ sudo docker stack services
  ```
  ### Eliminar una pila

  **docker stack rm [STACK]**

  Esta instrucción elimina la pila indicada.

  ```
  $ sudo docker stack rm helloWorld
  ```

  ## docker-compose.yml

  Como se mencionó arriba, un archivo _YAML_ de configuración es necesario para poder desplegar servicios en pilas a Docker Swarm. Para ver un ejemplo de este archivo, da click aquí.

  Todos los archivos _YAML_ de configuración de pila deben iniciar con la versión, la cual actualmente es 3, en formato _String_:

  ```
  version: '3'
  ```
  
  Después, entra la declaración de servicios que serán desplegados con la pila, iniciando la declaración con el tag _services_.
  Debajo del tag services, se declararán los nombres de cada servicio que será desplegado:

  ```
  services:
     service1:
     service2:
     service3:
  ```
  Dentro de cada servicio, se declararán las opciones específicas de ese servicio; como lo son la imagen del servicio, los puertos del servicio, los volúmenes del servicio y el ambiente del servicio entre otras cosas:

  ```
  services:
    db:
      image: mysql:5.7
      restart: always
      ports:
        - "4306:3306"
      volumes:
        - db_data:/var/lib/mysql
      environment:
        MYSQL_ROOT_PASSWORD: root_password
        MYSQL_DATABASE: database
        MYSQL_USER: user
        MYSQL_PASSWORD: password
  ```

