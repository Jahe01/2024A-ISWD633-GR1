# Redes
Las redes son un componente fundamental que permite la comunicación entre contenedores, así como la comunicación de los contenedores con el mundo exterior. 
![Imagen](imagenes/redes.PNG)
- Bridge: Esta es la red por defecto en Docker. Permite la comunicación entre contenedores en el mismo host. Cada contenedor conectado a la red bridge tiene una IP propia en la subred de la red bridge.
    -  Brige por default: Cuando se ejecuta un contenedor, Docker crea automáticamente una red de tipo bridge por default. Esta red se utiliza para permitir la comunicación entre contenedores en el mismo host. Cada contenedor conectado a esta red obtiene su propia dirección IP en la subred de la red bridge.
    - Bridge creada por nosotros: Un usuario también puede crear sus propias redes de tipo bridge en Docker. Esto puede ser útil para organizar y segmentar los contenedores de una aplicación de manera más controlada. Al crear una red bridge personalizada, se puede especificar un rango de direcciones IP y otras configuraciones de red específicas. Los contenedores conectados a esta red utilizarán las direcciones IP de la subred definida por el usuario.
- Host: Con esta red, los contenedores comparten la red del host en lugar de tener su propia interfaz de red. Esto puede mejorar el rendimiento de red, pero los contenedores pueden entrar en conflicto con los puertos del host si intentan utilizar los mismos puertos.
- None: Con esta red, se deshabilita la configuración de red. Los contenedores que usan esta red tienen su propia red de bucle invertido y no pueden comunicarse con otros contenedores a menos que se conecten explícitamente a una red.

### Crear una red de tipo bridge

```
docker network create <nombre red> -d bridge
```

### Crear un contenedor vinculado a una red

```
docker run -d --name <nombre contenedor> --network <nombre red> <nombre imagen>
```

### Para saber a qué red está conectado un contenedor

```
docker inspect <nombre contenedor>
```
ó
```
docker network inspect <nombre red> 
```

### Vincular contenedor a una red
```
docker network connect <nombre red> <nombre contenedor>
```

### Para desvincular un contenedor de una red
```
docker network disconnect <nombre red> <nombre contenedor>
```

### Para listar las redes existentes
```
docker network ls
```

### Crear los contenedores y las redes que se presentan en el esquema. Usar para todos los contenedores la imagen de nginx:alpine
![Imagen](imagenes/esquema-ejercicio-redes.PNG)
crea las redes net-curso01 y net-curso02
 ```
docker network create net-curso01 -d bridge
docker network create net-curso02 -d bridge
```
#Crear los Contenedores Vinculados a las Redes

Crear contenedor1 en net-curso01
```
docker run -d --name contenedor1 --network net-curso01 nginx:alpine
```
Crear contenedor2 en net-curso01
```
docker run -d --name contenedor2 --network net-curso01 nginx:alpine
```
Crear contenedor3 en net-curso01
```
docker run -d --name contenedor3 --network net-curso01 nginx:alpine
```
Crear contenedor4 en net-curso02:
```
docker run -d --name contenedor4 --network net-curso02 nginx:alpine
```
![Imagen](imagenes/con.PNG)

Verificar la Conexión de los Contenedores a las Redes
```
docker network inspect net-curso01
```
![Imagen](imagenes/in1.PNG)

```
docker network inspect net-curso02
```
![Imagen](imagenes/in2.PNG)

 listar todas las redes creadas en Docker
```
docker network ls
```
![Imagen](imagenes/li.PNG)

Listar los Contenedores y sus Redes
```
docker ps -a
```
![Imagen](imagenes/todo.PNG)

Detener y Eliminar los Contenedores que Están Utilizando las Redes
```
docker stop contenedor1 contenedor2 contenedor3 contenedor4
```
Eliminar los contenedores
```
docker rm contenedor1 contenedor2 contenedor3 contenedor4
```
Eliminar las redes
```
docker network rm net-curso01 net-curso02
```
