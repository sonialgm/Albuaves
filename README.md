# Albuaves

# Albuaves

Albuaves es un pequeño proyecto mascota ( *pet-project* ) , que pretende
de una manera sencilla plantear al alumnado todas las partes implicadas
en una Solución Software basada en la arquitectura *Cliente-Servidor*.

Por una parte tendremos una base de datos en `SQLite` que editaremos de manera
sencilla con `sqlitebrowser` y que usaremos como persistencia en el lado 
del servidor.

Serviremos una API Rest, programada en PHP, por ahora se plantea con dos únicas
funciones: 

### Listar todas las aves

### Listar un ave a partir de un `id_ave` dado

## Software Requerido

* sqlitebrowser
* php-sqlite3

### Comandos para la instalación en máquinas de desarrollo

```bash
sudo apt update; sudo apt install sqlitebrowser php-sqlite3
```

## URLs de interés

### JSON.org

Podemos encontrar más información acerca de JSON.org en la página de 
GitHub del desarrollador principal.

https://github.com/stleary/JSON-java

-----

### Cambios realizados

El programa inicial presentaba algunos errores que he modificado. 
- En la terminal se imprimía el resultado sin formato (`System.out.println(response);`).  
  Comenté la línea para que solo se mostrase el resultado formateado.

- Las rutas de las imágenes eran incorrectas. Para modificarlas, ejecuté en SQLite:

  ```sql
  sqlite3 ./db/albuaves.db;
  UPDATE birds
  SET img_url = REPLACE(img_url, './imgs/aves//', './imgs/')
  WHERE img_url LIKE './imgs/aves//%';
  ```

No funcionaba el **GET** a partir del *id* de las aves.  
Modifiqué la siguiente línea en `api.php`:

```php
$stmt->bindValue(':bird_id', $id, SQLITE3_INTEGER);
```

### Ejecución y resultados

- **Cliente: Java ejecutándose en la terminal:**

  ```bash
  javac -cp .:json-20250517.jar SearchBirdsAPI.java
  java -cp .:json-20250517.jar SearchBirdsAPI
  ```
  
- **API en el navegador:**  
  1. Iniciar el servidor mediante `run-api.server.sh`.  
  2. Comprobar el funcionamiento de la API en el navegador:  
     - `http://localhost:9191/api.php`  
     - `http://localhost:9191/api.php?bird_id=1` (si filtramos por ID, en este ejemplo el 1)


En las capturas de pantalla de este repositorio se puede observar el resultado del programa.
