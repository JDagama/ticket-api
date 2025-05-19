# Ticket API

Una API RESTful para la gestión de tickets de soporte.

## 🛠 Tecnologías usadas

- Java 17
- Spring Boot
- PostgreSQL
- Maven

## 🚀 Cómo ejecutar localmente

### Requisitos

- Java 17
- PostgreSQL 16
- Maven
  
### Compilar & Ejecutar Tests
 Para compilar el proyecto y ejecutar los tests, utiliza los siguientes comandos:

```sh
./mvnw clean install
```

Esto compilará el código y ejecutará todas las pruebas unitarias y de integración.

Si solo deseas ejecutar los tests sin compilar el jar final:

```sh
./mvnw test
```

Puedes ver los reportes de cobertura generados por JaCoCo en `target/site/jacoco/index.html` después de ejecutar:

```sh
./mvnw verify
```

> **NOTA:** Si no cuentas con una base de datos PostgreSQL, puedes usar la base de datos H2 agregando el siguiente parámetro al ejecutar los tests o la aplicación:
>
> ```sh
> ./mvnw test -Dspring.profiles.active=h2
> ```
> o para ejecutar la aplicación:
> ```sh
> ./mvnw spring-boot:run -Dspring-boot.run.profiles=h2
> ```


### Configuración

1. Crea una base de datos llamada `ticket` y un usuario con permisos:
   ```sql
   CREATE USER tm_db_user WITH PASSWORD 'dbadmin1519$';
   CREATE DATABASE ticket OWNER tm_db_user;
   GRANT ALL PRIVILEGES ON DATABASE ticket TO tm_db_user;
   ```
2. Actualiza el archivo `application.properties` si es necesario:
   ```properties
   spring.datasource.url=jdbc:postgresql://localhost:5432/ticket
   spring.datasource.username=tm_db_user
   spring.datasource.password=dbadmin1519$
   ```

### Ejecuta el proyecto
   ```properties
   ./mvnw spring-boot:run
   ```
   Si no cuenta con una DB Postgresql puede usar la DB H2 local
      ```properties
   ./mvnw spring-boot:run -Dspring-boot.run.profiles=h2
   ```


## 📫 Endpoints principales

| Método | Ruta           | Descripción              |
|--------|----------------|--------------------------|
| POST   | `/tickets`     | Crea un nuevo ticket     |
| GET    | `/tickets`     | Lista todos los tickets  |
| GET    | `/tickets/{id}`| Obtiene un ticket por ID |
| PUT    | `/tickets/{id}`| Actualiza un ticket      |
| DELETE | `/tickets/{id}`| Elimina un ticket        |

## 🧪 Pruebas

Este proyecto puede probarse fácilmente usando la extensión [REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) de VSCode.

1. Instala la extensión si aún no la tienes.
2. Abre el archivo `api.http` que se encuentra en la raíz del proyecto.
3. Haz clic en `Send Request` sobre las peticiones para probar los endpoints directamente desde VSCode.

## 🧪 Verificación en base de datos

Puedes verificar que los tickets hayan sido registrados correctamente ejecutando una consulta SQL directamente en tu base de datos PostgreSQL:
   ```sql
   SELECT * FROM ticket;
   ```
Asegúrate de conectarte como el usuario que creaste (`ticket_user`) y sobre la base de datos `ticket`. Puedes usar herramientas como `psql`, DBeaver o PgAdmin.