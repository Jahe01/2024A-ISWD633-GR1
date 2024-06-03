# VOLUMEN TIPO HOST
Un volumen host (o bind mount) es un tipo de volumen donde se monta un directorio o archivo específico del sistema de archivos del host en un contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```

### Crear un volumen tipo host con la imagen nginx:alpine, para la ruta carpeta host: directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html esta ruta se obtiene al revisar la se obtiene desde la documentación
![Volúmenes](imagenes/volumen-host.PNG)

Se debe de crear con puertos 

```
docker run -d --name mi_nginx_container -p 8080:80 -v ./html:/usr/share/nginx/html nginx:alpine
```


### ¿Qué sucede al ingresar al servidor de nginx?
Al ingresar al servidor de nginx se muestra la siguiente imagen
![Imagen](imagenes/A.JPG)
error 403 Forbidden

### ¿Qué pasa con el archivo index.html del contenedor?
Se abre
![Imagen](imagenes/B.JPG)


### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de nginx/html
### ¿Qué sucede al ingresar al servidor de nginx?
Se muestra la pantalla del template

### Eliminar el contenedor
```
 docker rm -f mi_nginx_container
```

### ¿Qué sucede al crear nuevamente el mismo contenedor con volumen de tipo host a los directorios definidos anteriormente?

Cuando creas nuevamente el mismo contenedor Docker con el mismo volumen de tipo host a los mismos directorios definidos anteriormente, básicamente estás recreando el mismo entorno de servidor web Nginx con el mismo contenido en la carpeta html.

### ¿Qué hace el comando pwd?
te devolverá /home/usuario/documentos, mostrando la ruta completa del directorio en el que te encuentras. Este comando es útil para verificar rápidamente en qué ubicación estás trabajando en la estructura de directorios del sistema de archivos.

Si quieres incluir el comando pwd dentro de un comando de Docker, lo puedes hacer de diferentes maneras dependiendo del shell que estés utilizando.


### Volumen tipo host usando PWD y PowerShell
```
docker run -d --name <nombre contenedor> --publish published=<valorPuertoHost>,target=<valor> -v ${PWD}/<ruta relativa>:<ruta absoluta> <nombre imagen>:<tag> 
```

### Volumen tipo host usando PWD (Git Bash)

```
docker run -d --name <nombre contenedor> --publish published=<valorPuertoHost>,target=<valor> -v $(pwd -W)/html:/usr/share/nginx/html <nombre imagen>:<tag> 
```

### Volumen tipo host usando PWD (en Linux)

```
docker run -d --name <nombre contenedor> --publish published=<valorPuertoHost>,target=<valor> -v $(pwd)/html:/usr/share/nginx/html <nombre imagen>:<tag> 
```

