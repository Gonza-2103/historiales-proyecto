# Microservicio de Historial ('historiales')

## Integrantes
* **Gonzalo Hormazábal**
* **Geraldinne González**


## Descripción
Módulo transversal inmutable encargado del registro histórico de trazas y auditoría del ecosistema. Almacena las huellas digitales de quién realizó qué acción y cuándo.

* **Puerto:** `8089`
* **Base de Datos:** `historiales_db` (MySQL)


## Funcionalidades Clave
* Centralización de logs de acciones críticas (Creación de categorías, ofertas, etc.).
* Manejo de `GlobalExceptionHandler` unificado que inyecta nombres de excepción formales en las respuestas.
* Marcas de tiempo automáticas para auditorías forenses mediante eventos JPA.


## Configuración (`application.properties`)
* server.port=8089
* spring.datasource.url=jdbc:mysql://localhost:3306/historiales_db
* spring.datasource.username=root
* spring.datasource.password=
* spring.jpa.hibernate.ddl-auto=update
* logging.level.cl.sda1085.historiales=DEBUG


## Pasos para Ejecutar

### 1. Preparación de la Base de Datos
Antes de ejecutar el servicio, crear la conexión a la base de datos de MySQL (XAMPP) corriendo en el puerto 3306 y con el nombre 'historiales_db'.

### 2. Verificación de Credenciales
Revisar que el archivo application.properties tenga por defecto, usuario root y contraseña vacía.

### 3. Lanzamiento del Microservicio
Ejecutar (run) la clase principal con la anotación @SpringBootApplication (HistorialesApplication.java).

### 4. Reglas de Seguridad
Al consumir los endpoints en Postman, ten en cuenta el comportamiento de la cadena de filtros de seguridad:

* Registro de Trazas (POST /api/historiales): Al ser un servicio de auditoría interna alimentado por otros componentes, los endpoints de escritura aceptan peticiones internas automáticas del sistema (No Auth bajo red local interna).
* Acceso a Logs de Auditoría (GET /api/historiales): Al contener información sensible de las operaciones e interacciones del ecosistema, su lectura en Postman está bloqueada y requiere Basic Auth estricto con rol de ADMIN.
