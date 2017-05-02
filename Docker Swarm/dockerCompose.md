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
