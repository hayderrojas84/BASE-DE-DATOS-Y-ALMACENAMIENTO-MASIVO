# Librería Database Project

## Descripción

Este proyecto consiste en la creación y gestión de una base de datos relacional para una librería ficticia utilizando MySQL. La base de datos está diseñada para almacenar y manejar información sobre autores, libros, clientes y pedidos. El proyecto incluye el uso de comandos DDL (Data Definition Language) y DML (Data Manipulation Language), así como consultas SQL avanzadas y funciones SQL para operar y analizar los datos.

## Estructura de la Base de Datos

La base de datos consta de cuatro tablas principales:

1. **Autores**
   - `id_autor` (INT, PRIMARY KEY, AUTO_INCREMENT)
   - `nombre` (VARCHAR(100), NOT NULL)
   - `apellido` (VARCHAR(100), NOT NULL)
   - `nacionalidad` (VARCHAR(50))

2. **Libros**
   - `id_libro` (INT, PRIMARY KEY, AUTO_INCREMENT)
   - `titulo` (VARCHAR(200), NOT NULL)
   - `genero` (VARCHAR(100))
   - `precio` (DECIMAL(10,2))
   - `id_autor` (INT, FOREIGN KEY)

3. **Clientes**
   - `id_cliente` (INT, PRIMARY KEY, AUTO_INCREMENT)
   - `nombre` (VARCHAR(100), NOT NULL)
   - `apellido` (VARCHAR(100), NOT NULL)
   - `correo` (VARCHAR(100), UNIQUE, NOT NULL)

4. **Pedidos**
   - `id_pedido` (INT, PRIMARY KEY, AUTO_INCREMENT)
   - `id_cliente` (INT, FOREIGN KEY)
   - `id_libro` (INT, FOREIGN KEY)
   - `fecha_pedido` (DATE)

## Instalación

Para utilizar esta base de datos en tu entorno local, sigue los siguientes pasos:

1. Clona este repositorio:
    ```bash
    git clone https://github.com/tuusuario/libreria-db.git
    ```

2. Navega al directorio del proyecto:
    ```bash
    cd libreria-db
    ```

3. Carga el archivo `libreria.sql` en tu servidor MySQL:
    ```bash
    mysql -u usuario -p libreria < libreria.sql
    ```

4. Accede a la base de datos en MySQL:
    ```bash
    mysql -u usuario -p
    USE Libreria;
    ```

## Uso

Una vez cargada la base de datos, puedes ejecutar las consultas y comandos SQL incluidos en los archivos del proyecto para interactuar con los datos.

### Ejemplos de Consultas SQL

- **Consultar todos los libros con el nombre del autor:**
    ```sql
    SELECT Libros.titulo, Autores.nombre, Autores.apellido 
    FROM Libros 
    INNER JOIN Autores ON Libros.id_autor = Autores.id_autor;
    ```

- **Consultar todos los pedidos realizados por un cliente específico:**
    ```sql
    SELECT Pedidos.id_pedido, Clientes.nombre, Clientes.apellido, Libros.titulo, Pedidos.fecha_pedido 
    FROM Pedidos
    INNER JOIN Clientes ON Pedidos.id_cliente = Clientes.id_cliente
    INNER JOIN Libros ON Pedidos.id_libro = Libros.id_libro
    WHERE Clientes.correo = 'juan.perez@example.com';
    ```

- **Calcular el total de ventas:**
    ```sql
    SELECT SUM(Libros.precio) AS Total_Ventas 
    FROM Pedidos 
    INNER JOIN Libros ON Pedidos.id_libro = Libros.id_libro;
    ```

### Funciones y Operadores SQL

- **Uso de la función CONCAT para combinar el nombre y apellido del autor:**
    ```sql
    SELECT CONCAT(nombre, ' ', apellido) AS Nombre_Completo 
    FROM Autores;
    ```

- **Uso de operadores para obtener libros con precio mayor a 15:**
    ```sql
    SELECT * FROM Libros WHERE precio > 15;
    ```

- **Uso de la función COUNT para contar el número de libros de cada género:**
    ```sql
    SELECT genero, COUNT(*) AS Numero_Libros 
    FROM Libros 
    GROUP BY genero;
    ```

## Contribuciones

Las contribuciones son bienvenidas. Si tienes ideas para mejorar el proyecto o encuentras algún problema, por favor abre un issue o envía un pull request.

