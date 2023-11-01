# RETO SAN MYSQL

1. INSTALA EL SGBD MYSQL Y EL CLIENTE WORKBRENCH
2. CADA EJERCICIO DE CADA ITERACIÓN TIENE UN VIDEO QUE HAY QUE VER ANTES O DURANTE SE VA RESOLVIENDO.

## ITERATION 1 - MODELADO

### EJERCICIO 1 - MODELO ER

**VIDEO LESSION**: https://drive.google.com/file/d/1frRZgEE5LAZLNqUKzVSt5rTtSRRKADHk/view

**ENTREGABLE**: Imagen con modelo ER.

##### DESCRIPCIÓN DEL PROBLEMA

###### Spotify

Vamos a tratar de hacer un modelo sencillo de cómo sería la base de datos necesaria para Spotify.

- Existen dos tipos de usuarios: usuario *free* y usuario *premium*.
- De cada usuario guardamos un id único, *email*, *password*, nombre de usuario, fecha de nacimiento, sexo, país, código postal.
- Los usuarios *premium* realizan suscripciones. Los datos necesarios que habrá que guardar para cada suscripción son: fecha de inicio de la suscripción, fecha de renovación del servicio.
- Una suscripción tiene muchos pagos asociados. De cada pago se almacena un identificador, una fecha, una cantidad y una forma de pago, que puede ser mediante tarjeta de crédito o PayPal.
- De las tarjetas de crédito guardamos el número de tarjeta, mes y año de caducidad y el código de seguridad. De los usuarios que pagan con PayPal guardamos el nombre de usuario de PayPal.
- Un usuario puede crear muchas *playlists*. De cada *playlist* guardamos un título, el número de canciones que contiene, un identificador único y una fecha de creación.
- Cuando un usuario borra una *playlist* no se borra del sistema, sino que se marca como que ha sido eliminada. De este modo el usuario puede volver a recuperar sus *playlists* en caso de que las haya eliminado por error. Es necesario almacenar la fecha en la que una *playlist* ha sido marcada como eliminada.
- Podemos decir que existen dos tipos de *playlists*: activas y borradas.
- Una *playlist* que está activa puede ser compartida con otros usuarios, esto quiere decir que otros usuarios pueden añadir  canciones en ella. En una lista compartida nos interesa saber qué usuario ha sido el que ha añadido cada canción y en qué fecha lo hizo.
- Una canción sólo puede pertenecer a un único álbum. Un álbum puede contener muchas canciones. Un álbum ha sido publicado por un único artista. Un artista puede haber publicado muchos álbumes.
- De cada canción guardamos un id único, un título, una duración y el número de veces que ha sido reproducida por los usuarios de Spotify.
- De cada álbum guardamos un id único, título, año de publicación y una imagen con la portada.
- De cada artista guardamos un id único, nombre y una imagen del artista.
- Un usuario puede seguir a muchos artistas.
- Un artista puede estar relacionado con otros artistas que hagan música parecida. De modo que Spotify pueda mostrarnos un listado de artistas relacionados con los artistas que nos gustan.
- También nos interesa guardar cuáles son los álbumes y las canciones favoritas de un usuario. Un usuario puede seleccionar muchos álbumes y muchas canciones como favoritas.

### EJERCICIO 2 - DDL

**VIDEO** **LESSON** : https://drive.google.com/file/d/13KFChigU8hR6MsMx6F2oWSYuhaVRGUZR/view

**ENTREGABLE**: ARCHIVO .sql con las queries SQL DDL que generan la base de datos y sus tablas para el modelo ER del ejericico 1.

###### DOC & GUIDES

https://www.mysqltutorial.org/mysql-basics/

- SECTION 9 - 10 - 11 - 12

## ITERATION 2 - DML

#### EJERCICIO 1 - SELECT - FROM - ORDER BY

**VIDEO LESSON:** https://drive.google.com/file/d/1msFuyAbA70FrEg4w_90-EOuRDjRFPEly/view

**ENTREGABLE**: archivo .sql con las consultas para obtener los siguientes conjuntos de registros:

**DB A IMPORTAR**:

```sql
DROP DATABASE IF EXISTS tienda;
CREATE DATABASE tienda CHARACTER SET utf8mb4;
USE tienda;

CREATE TABLE fabricante (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL
);

CREATE TABLE producto (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  precio DOUBLE NOT NULL,
  id_fabricante INT UNSIGNED NOT NULL,
  FOREIGN KEY (id_fabricante) REFERENCES fabricante(id)
);

INSERT INTO fabricante VALUES(1, 'Asus');
INSERT INTO fabricante VALUES(2, 'Lenovo');
INSERT INTO fabricante VALUES(3, 'Hewlett-Packard');
INSERT INTO fabricante VALUES(4, 'Samsung');
INSERT INTO fabricante VALUES(5, 'Seagate');
INSERT INTO fabricante VALUES(6, 'Crucial');
INSERT INTO fabricante VALUES(7, 'Gigabyte');
INSERT INTO fabricante VALUES(8, 'Huawei');
INSERT INTO fabricante VALUES(9, 'Xiaomi');

INSERT INTO producto VALUES(1, 'Disco duro SATA3 1TB', 86.99, 5);
INSERT INTO producto VALUES(2, 'Memoria RAM DDR4 8GB', 120, 6);
INSERT INTO producto VALUES(3, 'Disco SSD 1 TB', 150.99, 4);
INSERT INTO producto VALUES(4, 'GeForce GTX 1050Ti', 185, 7);
INSERT INTO producto VALUES(5, 'GeForce GTX 1080 Xtreme', 755, 6);
INSERT INTO producto VALUES(6, 'Monitor 24 LED Full HD', 202, 1);
INSERT INTO producto VALUES(7, 'Monitor 27 LED Full HD', 245.99, 1);
INSERT INTO producto VALUES(8, 'Portátil Yoga 520', 559, 2);
INSERT INTO producto VALUES(9, 'Portátil Ideapd 320', 444, 2);
INSERT INTO producto VALUES(10, 'Impresora HP Deskjet 3720', 59.99, 3);
INSERT INTO producto VALUES(11, 'Impresora HP Laserjet Pro M26nw', 180, 3);
```

1. Lista el nombre de todos los productos que hay en la tabla `producto`.
2. Lista los nombres y los precios de todos los productos de la tabla `producto`.
3. Lista todas las columnas de la tabla `producto`.
4. Lista los nombres de los fabricantes ordenados de forma ascendente.
5. Lista los nombres de los fabricantes ordenados de forma descendente.
6. Lista los nombres de los productos ordenados en primer lugar por el nombre de forma ascendente y en segundo lugar por el precio de forma descendente.

#### EJERCICIO 2 - FILTROS Y FUNCIONES

**VIDEO LESSSON**: https://drive.google.com/file/d/1-9snGTEh5JYdSwhdmO1Z9h3ft3UDBHkl/view

MISMA DB EJERCICIO 1

1. Lista el nombre de los productos, el precio en euros y el precio en dólares estadounidenses (USD). Utiliza los siguientes alias para las columnas: `nombre de producto`, `euros`, `dólares`.
2. Lista el nombre de todos los fabricantes en una columna, y en otra columna obtenga en mayúsculas los dos primeros caracteres del nombre del fabricante.
3. Lista los nombres y los precios de todos los productos de la tabla `producto`, truncando el valor del precio para mostrarlo sin ninguna cifra decimal.
4. Lista el identificador de los fabricantes que tienen productos en la tabla `producto`.

5. Lista el identificador de los fabricantes que tienen productos en la tabla `producto`, eliminando los identificadores que aparecen repetidos.

6. Lista el nombre de los productos que tienen un precio menor o igual a 120€.
7. Lista el nombre de los productos que **no tienen** un precio mayor o igual a 400€.
8. Lista los nombres de los fabricantes cuyo nombre sea de 4 caracteres.

9. Devuelve una lista con el nombre de todos los productos que contienen la cadena `Monitor` en el nombre y tienen un precio inferior a 215 €.
10. Lista el nombre y el precio de todos los productos que tengan un precio mayor o igual a 180€. Ordene el resultado en primer lugar por el precio (en orden descendente) y en segundo lugar por el nombre (en orden ascendente).

#### EJERCICIO 2 - FILTROS Y FUNCIONES

## ITERACIÓN 3 DRIVER
