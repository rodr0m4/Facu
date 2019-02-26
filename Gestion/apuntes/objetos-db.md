# Objetos de la DB

## Tablas

Unidad básica de almacenamiento de datos, en filas y columnas. Son permanentes y tienen un identificador único dentro de un schema.
Cada columna tiene metadata: nombre, tipo de dato.

### Temporales

No se registran en el DD. No se les puede hacer ALTER. Si se pueden eliminar y crearle índices temporales. Puede elegirse no generar logs transaccionales para las mismas.

#### Tipos

**De sesión (locales):** Son visibles solo para sus creadores dentro de una misma sesión a una instancia del motor de la DB. Se eliminan cuando el usuario se desconecta o decide eliminar la tabla.

**Globales:** Visibles para cualquier usuario y sesión una vez creadas. Su eliminación depende del RBDMS.


**De creación explícita:** Se dan por utilizar CREATE, se indica su nombre, campos, tipos de dato y restricciones.

**De creación implícita:** Pueden generarse a partir de una instrucción de SELECT.

#### Rationale

**Como almacenamiento intermedio para consultas MUY grandes**

Por ejemplo, joineando 8 tablas, ya que muchas veces queries con muchos joins pueden ser poco performantes, se divide una query grande en muchas pequeñas.

**Para optimizar accesos a una consulta varias veces en una aplicación**

En vez de repetir varias veces una query que voy a reutilizar en el contexto de un SP, creo una tabla intermedia donde dumpeo el resultado la primera vez.

**Para almacenar resultados intermedios en una aplicación**

Quiero ir modificando información (resultados intermedios de una operación compleja, por ejemplo), sin modificar tablas reales de la DB. Al final del mismo, paso los valores de la tabla temporal a una tabla real.

### Anidadas

Se puede crear una columna en una tabla cuyo tipo de dato sea otra tabla.

## Constraints

*Integridad de Entidad:* asegurar unicidad en una tabla. Se utilizan las PKs (que en general no admiten NULLs).
