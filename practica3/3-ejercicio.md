## Esquema para el ejercicio
![Imagen](imagenes/esquema-ejercicio3.PNG)

### Crear red net-wp
```
docker network create net-wp

```
lista todas las redes disponibles en Docker:
```
docker network ls
```

Por ejemplo, para conectar un contenedor a la red net-wp, puedes utilizar el siguiente comando al crear el contenedor:
```
docker run -d --name mi_contenedor --network net-wp imagen_contenedor
```
```
docker run -d --name mysql --network net-wp -e MYSQL_ROOT_PASSWORD=wordpress -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wordpress -e MYSQL_PASSWORD=wordpress -v C:/ejercicio3/db:/var/lib/mysql mysql:8

```
```
docker run -d --name wordpress --network net-wp -e WORDPRESS_DB_HOST=mysql:3306 -e WORDPRESS_DB_USER=wordpress -e WORDPRESS_DB_PASSWORD=wordpress -e WORDPRESS_DB_NAME=wordpress -p 9500:80 -v C:/ejercicio3/www/html:/var/www/html wordpress
```


### Para que persista la información es necesario conocer en dónde mysql almacena la información.
En el esquema del ejercicio la carpeta contenedor (b) es /var/www/html. Ruta carpeta host: .../ejercicio3/www.
Ruta carpeta host: .../ejercicio3/db


### ¿Qué contiene la carpeta db del host?
La carpeta esta vacia
![Imagen](imagenes/s.JPG)


### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
Comando para Crear el Contenedor con la Imagen de WordPress
```
docker run -d --name server-wordpress \
  -e WORDPRESS_DB_HOST=server-postgres \
  -e WORDPRESS_DB_USER=user_drupal \
  -e WORDPRESS_DB_PASSWORD=12345 \
  -e WORDPRESS_DB_NAME=db_drupal \
  -v .../ejercicio3/www:/var/www/html \
  --network net-wp \
  wordpress

```
### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?

Se encuentrar los archivos de mysql

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/)
En el esquema del ejercicio la carpeta contenedor (b) es /var/www/html. Ruta carpeta host: .../ejercicio3/www.
Ruta carpeta host: .../ejercicio3/www

Personalización y Persistencia
Personalizar la Apariencia y Agregar una Entrada

Ingresa a tu instalación de WordPress a través del navegador (usualmente en http://localhost o en el puerto que hayas configurado) y personaliza la apariencia. Agrega una entrada desde el panel de administración de WordPress.

Eliminar el Contenedor y Crearlo Nuevamente
```
docker rm -f server-wordpress

docker run -d --name server-wordpress \
  -e WORDPRESS_DB_HOST=server-postgres \
  -e WORDPRESS_DB_USER=user_drupal \
  -e WORDPRESS_DB_PASSWORD=12345 \
  -e WORDPRESS_DB_NAME=db_drupal \
  -v .../ejercicio3/www:/var/www/html \
  --network net-wp \
  wordpress

```

¿Qué ha sucedido? Al eliminar el contenedor y crearlo nuevamente, si has configurado correctamente el volumen persistente (montaje de la carpeta /var/www/html a la ruta en el host .../ejercicio3/www), la personalización de la apariencia y las entradas que agregaste deberían persistir. Esto es porque los datos se almacenan en el volumen que mapeaste a la carpeta del host, permitiendo que los cambios realizados se mantengan aunque el contenedor sea eliminado y recreado.



