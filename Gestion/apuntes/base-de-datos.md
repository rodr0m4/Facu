# Base de Datos

Conjunto de datos persistentes e interrelacionados utilizado en sistemas de aplicación, almacenados independientemente y sin redundancia.

**RDBMS:** programa que permite administrar bases de datos, también llamada Motor. Interpreta y ejecuta SQL, así nos abstraemos de la representación física de los datos.

**Procesos:** controlan el RDBMS, proveen funciones de seguridad, integridad, operación, organización interna entre otros.

**Memoria compartida:**
  * Cachear datos para tener acceso más rápido.
  * Mantener y controlar recursos necesarios para los procesos.
  * Proveer mecanismos de comunicación para interactuar con otras aplicaciones y coordinar actividades.

**Unidades de disco:**
  * Uno o más discos asignados a la DB.
  * Contiene metadata de la DB.

## Arquitectura ANSI/SPARC

### Nivel Externo / VISTAS

Percepción de los usuarios respecto de la DB. Un usuario puede ser un usuario final, programador o DBA. La percepción de los usuarios es de vista externa (como ve un usuario la DB).

### Nivel Conceptual / LÓGICO

Representa de forma 'entendible' de toda la información contenida en la DB. Describe los datos de toda la organización.
Se define mediante un esquema conceptual. Se describe en DDL. Contiene definiciones del contenido de la base, tipos de dato, restricciones, reglas de integridad, etc.

### Nivel Interno / FÍSICO

Define como se almacenan los datos en el disco, representación de bajo nivel de los datos. Estructuras en disco y en memoria, se definen métodos de acceso, en que secuencia física se encuentran los registros, etc.

### Transformación Externa -> Conceptual

Dada una vista externa, realiza la transformación a la representación conceptual.

### Transformación Conceptual -> Física

Define como se almacenan las filas y columnas conceptuales físicamente.


## Diccionario de Datos

Conjunto de tablas de los objetos del sistema, define la metadata de los mismos. No pueden ser alteradas por los usuarios. Tiene las definiciones de las tablas, sus tipos de datos, y relaciones.

**Sentencias relacionadas:** CREATE, ALTER, DROP.

# Funciones del motor

## Seguridad

Implica que cosas tienen permitidas los usuarios de la db. Las DBs tienen el llamado catálogo (entidades e interrelaciones entre las mismas).
**Entidades:**
  * Usuarios
  * Roles y perfiles
  * Acciones a realizar
  * Objetos de la DB.
**Sentencias:** GRANT y REVOKE.
**Objetos relacionados con la seguridad:** vistas, triggers, SPs, sinónimos, entre otros.

## Integridad de datos

Constraints, triggers, índices, vistas y SPs

## Consistencia

* Transacciones: conjunto de sentencias que se ejecutan atómicamente. Garantiza que, o bien el conjunto se ejecute de forma correcta, o vuelva el estado de la db de antes de ejecutar las mismas. Comienzo con BEGIN TRANSACCTION, para confirmarla COMMITEO, para volver hacia atrás hago ROLLBACK.
* Logs transaccionales: registro donde el motor guarda las operaciones que fueron realizadas sobre la db.
* Recovery: algunas formas:
  - Retorna la db al anterior estado consistente (utilizando checkpoints).
  - Usando logs transaccionales, hacer "rolling forward" o "rolling back"

## ACID (Atomicity, Consistency, Isolation, Durability)

### Backup y Restore

*Backup* es una copia total y parcial de la información de la DB que debe ser guardado en un medio de almacenamiento vacío. *Restore* es tomar un backup y restaurar los datos.

*Backup diferencial acumulativo / incremental:* solo se guardan las modificaciones a partir de cierta fecha.
*Backup completo:* se guardan todos los datos.
*Backup en caliente:* se realiza mientras el aplicativo está en uso.
*Backup en frío:* se realiza con el aplicativo bajo.
*Backup de Logs Transaccionales:* se realizan sobre los logs de transacciones.

Estrategias de backup: *Diferencial acumulativo* desde un día, todo el backup, y *Diferencial incremental* se da de a pocos días, deltas más pequeños.


## Niveles de Aislamiento

### Read Uncomitted

No lockea en el select, mejora el rendimiento pero afecta la integridad en cuanto a que existen lecturas sucias y no existen lecturas repetibles. Puede haber lecturas sucias, no repetibles y fantasmas.

### Read Committed (default en general)

Asegura que no haya lecturas sucias. No asegura lecturas repetibles, ya que una vez que leyó los datos, libera el lock (*en criollo* dentro del contexto de una misma transacción, dos selects iguales podrían dar distinto resultado).

### Repeatable Read

Asegura lecturas limpias y repetibles, pero no evita las fantasmas. Lockea los selects de todos los registros consultados durante una transacción (Bloquea otras transacciones que quieran modificar el recurso en cuestión).
Las lecturas fantasmas se mantienen ya que no lockea nuevos registros que puedan ser insertados luego de iniciar la transacción (*en criollo* como no lockea la tabla entera, podés insertar registros nuevos, y luego modificar los mismos, y dentro de la TX van a cambiar).

### Serializable Read

Trata de bloquear un rango de filas (todas las que consulte una consulta con un where). Si no lo puede hacer bloquea toda la tabla.


Todas estas pueden llegar a provocar un deadlock (a excepción de read uncomitted :P).

## Otras características de la DB 

Pueden guardar un log de como se utilizó para futuras consultas. También loguean información del sistema (para diagnosticar por qué se dio un fallo, por ejemplo). Dump de cosas:

Mirroring de Discos Data Replication Data Encryption Monitoring Features
Event Alarms
Optimizador de Queries Particionamiento de Tablas e Indices
