# Tienda Remeras
## Descripción
Tienda Remeras es una página web de ejemplo en la cual se pueden observar las remeras que hay en la base de datos, agregar más remeras, categorías y cuentas. No es una tienda oficial, solo es un proyecto para incluirlo en mi portfolio.
IMPORTANTE: Esta página web no cuenta con un responsive design para celulares, por lo cual es recomendable verla en PC.


## Lenguajes utilizados
* HTML
* CSS
* PHP
* POO
* MVC
* SQL


## Agregar la base de datos (Obligatorio)
Para visualiar y utilizar la página se debe crear la base de datos.
Copie y pegue el siguiente código en su base de datos:
```
CREATE DATABASE tienda_remeras;
USE tienda_remeras;

CREATE TABLE usuarios(
id              int(255) auto_increment not null,
nombre          varchar(100) not null,
apellidos       varchar(255),
email           varchar(255) not null,
password        varchar(255) not null,
rol             varchar(20),
imagen          varchar(255),
CONSTRAINT pk_usuarios PRIMARY KEY(id),
CONSTRAINT uq_email UNIQUE(email)  
)ENGINE=InnoDb;

INSERT INTO usuarios VALUES(NULL, 'Admin', 'Admin', 'admin@admin.com', 'contraseña', 'admin', null);

CREATE TABLE categorias(
id              int(255) auto_increment not null,
nombre          varchar(100) not null,
CONSTRAINT pk_categorias PRIMARY KEY(id) 
)ENGINE=InnoDb;

INSERT INTO categorias VALUES(null, 'Manga corta');
INSERT INTO categorias VALUES(null, 'Estampada');
INSERT INTO categorias VALUES(null, 'Manga larga');
INSERT INTO categorias VALUES(null, 'Musculosa');

CREATE TABLE productos(
id              int(255) auto_increment not null,
categoria_id    int(255) not null,
nombre          varchar(100) not null,
descripcion     text,
precio          float(100,2) not null,
stock           int(255) not null,
oferta          varchar(2),
fecha           date not null,
imagen          varchar(255),
CONSTRAINT pk_categorias PRIMARY KEY(id),
CONSTRAINT fk_producto_categoria FOREIGN KEY(categoria_id) REFERENCES categorias(id)
)ENGINE=InnoDb;


CREATE TABLE pedidos(
id              int(255) auto_increment not null,
usuario_id      int(255) not null,
departamento    varchar(100) not null,
localidad       varchar(100) not null,
direccion       varchar(255) not null,
coste           float(200,2) not null,
estado          varchar(20) not null,
fecha           date,
hora            time,
CONSTRAINT pk_pedidos PRIMARY KEY(id),
CONSTRAINT fk_pedido_usuario FOREIGN KEY(usuario_id) REFERENCES usuarios(id)
)ENGINE=InnoDb;

CREATE TABLE lineas_pedidos(
id              int(255) auto_increment not null,
pedido_id       int(255) not null,
producto_id     int(255) not null,
unidades        int(255) not null,
CONSTRAINT pk_lineas_pedidos PRIMARY KEY(id),
CONSTRAINT fk_linea_pedido FOREIGN KEY(pedido_id) REFERENCES pedidos(id),
CONSTRAINT fk_linea_producto FOREIGN KEY(producto_id) REFERENCES productos(id)
)ENGINE=InnoDb;
```
##### Nota: Este código está en "database/database.sql"


## Agregar usuario e iniciar sesión
1. Ir a registrarse aquí
2. Rellenar los campos y dar en "Registrarse"
3. Para iniciar sesión rellenar los campos que se encuentran en la izquierda


## Realizar pedido
1. Dar click en "Comprar" en la parte inferior de un producto
2. (OPCIONAL) Cambiar la cantidad de unidades del producto
3. Ir a "Hacer pedido"
4. Rellenar los campos del envío y confirmar el envío


## Hacer un usuario como administrador
Esto se debe hacer desde la base de datos de MySQL
En la tabla "usuarios" cambiar en el usuario el rol "user" por "admin"
Siendo administrador se puede: gestionar categorías, gestionar productos y gestionar los pedidos de los usuarios

## Imágenes de ejemplo
En "uploads/images" se encuentran imágenes de remeras de ejemplo para usarlas al agregar productos como administrador
