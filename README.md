# Albuaves

Albuaves es un pequeño proyecto mascota ( *pet-project* ) , que pretende de una manera sencilla plantear las partes implicadas en una Solución Software basada en la arquitectura *Cliente-Servidor*.

Por una parte tendremos una base de datos en `SQLite` con información sobre las aves, que editaremos de manera sencilla con `sqlitebrowser` y que usaremos como persistencia en el lado del servidor.

Serviremos una API Rest, programada en PHP, por ahora se plantea con dos únicas funciones: 

### Listar todas las aves

### Listar un ave a partir de un `id_ave` dado

---

## Software Requerido

* sqlitebrowser
* php
* php-sqlite3
* openjdk

## Comandos para la instalación

```bash
sudo apt update
sudo apt install sqlitebrowser php-sqlite3
```

---

## Tecnologías utilizadas
### Java (Cliente)
- Lenguaje trabajado previamente en clase.
- Fácil integración con librerías JSON.

### SQLite
- Base de datos ligera.
- Fácil de usar con **sqlitebrowser**.
- Dominio público.

### PHP (API REST)
- Conexión sencilla con SQLite mediante `php-sqlite3`.
- Ideal para pequeños endpoints.

### Bash (.sh)

---

## Estructura del proyecto

```text
Proyecto_Albuaves/
│
├── db/                     # Base de datos y scripts SQL
│   ├── albuaves-db-create.sql
│   ├── albuaves-tables-population.sql
│   └── albuaves.db
│
├── imgs/                   # Imágenes de las aves
│
├── java/
│   ├── BuscadorAvesCompiler.sh
│   ├── SearchBirdsAPI.java
│   └── json-20250517.jar
│
├── libs/                   # Librerías adicionales
│
├── php/                    # Código PHP de la API
│   └── api.php
│
└── run-api-server.sh       # Script para iniciar la API
```

---

## Cambios realizados

El programa inicial presentaba algunos errores que he modificado. 

1. Mejora de salida en Java
   En la terminal se imprimía el resultado sin formato (`System.out.println(response);`).
   Comenté la línea para que solo se mostrase el resultado formateado.

3. Corrección de las rutas de imágenes
   Las rutas de las imágenes eran incorrectas. Para modificarlas, ejecuté en SQLite:

  ```sql
  sqlite3 ./db/albuaves.db;
  UPDATE birds
  SET img_url = REPLACE(img_url, './imgs/aves//', './imgs/')
  WHERE img_url LIKE './imgs/aves//%';
  ```
3. Corrección del GET por ID en la API
   No funcionaba el **GET** a partir del *id* de las aves.
   Modifiqué la siguiente línea en `api.php`:

  ```php
  $stmt->bindValue(':bird_id', $id, SQLITE3_INTEGER);
  ```

---

## How-to: Tutorial de uso

### Preparar el entorno
```bash
sudo apt update
sudo apt install php php-sqlite3 sqlitebrowser default-jdk
```

### Iniciar el servidor API
```bash
./run-api-server.sh
```

### Compilar y ejecutar el cliente Java
```bash
cd java
javac -cp .:lib/json-20250517.jar SearchBirdsAPI.java
java -cp .:lib/json-20250517.jar SearchBirdsAPI
```

### Probar API en el navegador
`http://localhost:9191/api.php`
`http://localhost:9191/api.php?bird_id=1`

---

## Ejecución y resultados

### Cliente: Java ejecutándose en la terminal
  ```bash
  cd java
  javac -cp .:lib/json-20250517.jar SearchBirdsAPI.java
  java -cp .:lib/json-20250517.jar SearchBirdsAPI
  ```
<img width="1223" height="580" alt="Java_Terminal" src="https://github.com/user-attachments/assets/5f853500-a626-44e2-b8ea-a0962da02bf7" />

### API en el navegador
- Iniciar el servidor mediante `run-api.server.sh`.  
- Comprobar el funcionamiento de la API en el navegador:
     `http://localhost:9191/api.php`
       
       <img width="1214" height="700" alt="API_Navegador" src="https://github.com/user-attachments/assets/d9353cf1-b33d-4100-b629-9a59892b4b71" />

     GET filtrado por ID: Si filtramos por ejemplo el 1: `http://localhost:9191/api.php?bird_id=1`
       
       <img width="1214" height="441" alt="API_Navegador_GET" src="https://github.com/user-attachments/assets/36601b9a-4913-4e0d-9001-e5360633a58f" />



