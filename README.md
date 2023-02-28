# Enlazar odoo,base de datos y python

---

## Explicación Docker-Compose

```version: '3.1'```
>Aquí definimos la version del docker-compose

```services:```
>En este apartado se definiran los componentes y servicios de nuestro docker-compose. En este caso tenemos dos servicios
>el de *Odoo* y el de *PostgresQL*
---
```
   db: 
    image: postgres:13
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_PASSWORD=odoo
      - POSTGRES_USER=odoo
    ports:
      - "5430:5432"
    volumes:
      - dam22_odooklk3:/var/lib/postgresql/data
``` 
 

>La base de datos se compone por varios componentes, entre ellos la imagen,el entorno,los puertos y el volumen
---
* ```image: postgres:13```  
Imagen de PostgresQL version 13
* ```
  environment:
      - POSTGRES_DB=postgres
      - POSTGRES_PASSWORD=odoo
      - POSTGRES_USER=odoo
  ``` 
  En el apartado del entorno o *enviroment* en inglés, definimos el nombre de la base de datos, el usuario y la contraseña.
* ```
  ports:
      - "5430:5432"
  ```
  Mapeamos los puertos de 5432 a 5430.
* ```
  volumes:
      - dam22_odooklk3:/var/lib/postgresql/data
  ```
  Definimos el volumen donde se van a guardar los datos.
---
```
odoo:
    image: odoo:14.0
    container_name: dam22_odooklk3
    volumes:
      - ./conf:/etc/odoo
    ports:
      - "8069:8069"
    depends_on:
      - db
```

> En el apartado de Odoo se definen la imagen, el nombre del contenedor, los puertos, los volumenes y las condiciones
---
* ```
  image: odoo:14.0
  ```
  Definimos la imagen de Odoo y la versión.
* ```
  container_name: dam22_odooklk3
    ```
  Definimos el nombre del contenedor de Docker.
* ```
  volumes:
      - ./conf:/etc/odoo
  ```
  Mapeamos el directorio para en un futuro desarrollar y configurar desde Python.
* ```
  ports:
      - "8069:8069"
  ```
  Mapeamos los puertos que se van a usar para Odoo.
* ```
  depends_on:
      - db
  ```
  Condición para que Odoo no se inicie antes que la base de datos.
---

```
volumes:
  dam22_odooklk3:
  ```

>Como último definimos el volumen que va a usar Dockre y todos sus componentes.
  
  
