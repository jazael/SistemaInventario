# SistemaInventario

Sistema de escritorio para la gestión de inventario de una tienda de productos electrónicos. Este sistema permite a los usuarios registrar nuevos productos, consultar el stock disponible, actualizar información de productos y eliminar registros obsoletos. 
Utiliza **PostgreSQL** como base de datos y está desarrollado en **Java** con NetBeans.

## Requisitos previos

Antes de comenzar, asegúrate de tener los siguientes elementos instalados en tu sistema:

- [NetBeans IDE](https://netbeans.apache.org/download/index.html)
- [Java Development Kit (JDK) 20+](https://www.oracle.com/java/technologies/javase/jdk20-archive-downloads.html)
- [PostgreSQL](https://www.postgresql.org/download/)
- [JDBC Driver para PostgreSQL](https://jdbc.postgresql.org/download.html)

## Configuración de la Base de Datos

1. Instala PostgreSQL y crea una nueva base de datos para el sistema de inventario. Puedes usar las siguientes instrucciones de comandos SQL para configurar la base de datos:

```sql
CREATE DATABASE inventario;

-- Conectar a la base de datos
\c inventario;

CREATE TABLE public.usuarios (
	id serial4 NOT NULL,
	username varchar(50) NOT NULL,
	"password" varchar(50) NOT NULL,
	CONSTRAINT usuarios_pkey PRIMARY KEY (id),
	CONSTRAINT usuarios_username_key UNIQUE (username)
);


CREATE TABLE producto (
  id serial primary key,
  nombre VARCHAR(100),
  descripcion VARCHAR(300),
  precio numeric,
  stock numeric,
  unidadmedida VARCHAR(20),
  fechacreacion date NOT NULL DEFAULT CURRENT_DATE,
  fechamodificacion date NOT NULL DEFAULT CURRENT_DATE,
  estado boolean default true
);


CREATE TABLE movimiento (
  id serial primary key,
  producto_id integer,
  tipomovimiento VARCHAR(10),
  cantidad numeric,
  fecha date,
  responsable VARCHAR(100),
  fechacreacion date NOT NULL DEFAULT CURRENT_DATE,
  fechamodificacion date NOT NULL DEFAULT CURRENT_DATE,
  estado boolean default true,
  FOREIGN KEY (producto_id) REFERENCES producto(id)
);
```

2. Cambia el archivo de propiedades
- Ubicación del Archivo: Localiza el archivo database.properties en la raíz del proyecto.

- Modificar el Archivo: Abre database.properties y asegúrate de que contenga la siguiente configuración:

  database.properties

  user=postgres
  password=postgres
  chainjdbc=jdbc:postgresql://localhost:5432/postgres

  user: Nombre de usuario para conectarte a la base de datos.
  password: Contraseña del usuario.
  chainjdbc: URL de conexión a la base de datos PostgreSQL.

- Guardar Cambios: Guarda el archivo después de realizar las modificaciones.

3. Corre el proyecto

  Ejecutar el Proyecto:

    Haz clic derecho nuevamente sobre el nombre del proyecto.
    Selecciona Run.

  Interactuar con la Aplicación:

    La aplicación se abrirá y podrás interactuar con la interfaz gráfica.

4. Ejecución de Test
Ejecutar Pruebas Unitarias:

    Haz clic derecho sobre el proyecto en el panel de proyectos.
    Selecciona Test para ejecutar todas las pruebas unitarias.

Revisar Resultados:

    Los resultados de las pruebas aparecerán en la ventana de salida. Asegúrate de que todas las pruebas pasen.
<img width="860" alt="image" src="https://github.com/user-attachments/assets/026118ed-0a8a-4ad1-8986-e8fef8407b4d">
