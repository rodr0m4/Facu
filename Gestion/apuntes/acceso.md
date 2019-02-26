# Métodos de Acceso

Consiste en guardar los datos bajo claves unequívocas e únicas, para poder buscarlas en tiempo mínimo, y poder reemplazarlas rápidamente.

**Clave:** dato o conjunto de datos que identifica un registro. Si es parte del registro se dice que es interna, otherwise es externa.
**DUP KEY:** cuando voy a insertar con una clave que ya existe en la estructura.
**INVALID KEY:** cuando voy a buscar en la estructura una clave que no existe.

## Búsqueda secuencial

Voy revisando uno por uno los registros hasta encontrar el que matchee con la clave dada. Recién valida invalid_key cuando recorrió todo el archivo. Complejidad en peor caso es lineal (O(n)) y en el caso promedio es O(n/2)

## Búsqueda secuencial indexada

Tengo n tablas secundarias, que representan punteros a valores de la siguiente tabla, del estilo:

120 | 157 ---\
 |           |
120 | 140 | 157 | 175
 |     ------------|
120 | 121 | 130 | 140 | ....

Ocupa mucho más espacio, pero hace que las búsquedas séan mucho más rápidas.


## Hashing

No obtengo el dato a partir de la posición relativa del mismo con respecto a los otros (como en un árbol), si no que tengo una función que me va a dar la posición del mismo a partir de la clave.
En general aplico una función llamada de hash (mucha dispersión para valores similares, así queda bien distribuida la estructura), y luego se aplicaría una operación de % al valor resultante, para que el mismo entre entre los valores posibles de la estructura.
Que pasa cuando hay colisiones?
  * rehashing (se aplica otra fórmula, más simple, para resolver esos casos).
  * Hashing into buckets: en vez de que la estructura sea un vector de valores, es un vector de listas enlazadas, y simplemente debo recorrer esta para resolver las colisiones.

## Árbol B

Los hasheos, entre otras cosas, no permiten búsqueda por rangos, ni permiten un acceso performante secuencial.
Para esto se utiliza un árbol n-ario, para el cual su acceso es en `logn (1 + m)`, donde m es la cantidad total de claves, y n es el nivel del árbol.
No es una estructura de buena complejidad espacial, pero no importa, ya que en general se usa para acceder a datos guardados en disco, donde es más importante el tiempo que el espacio ocupado.

El árbol B es un árbol n-ario donde los datos siempre están en las hojas, siempre se mantiene equilibrado (todas las hojas al mismo nivel).

Sea T un árbol b de orden *r* y raíz *t*, verifica:

* Cada nodo tiene a lo sumo r hijos.
* Cada nodo, a excepción de t y las hojas, tiene al menos r/2 hijos.
* Todas las hojas están al mismo nivel.
* Si la raíz no es una hoja, tiene al menos dos hijos.
* Un nodo con r hijos tiene r - 1 claves.

La altura del árbol está acotada por: `h <= 1 + log(r/2+1) ((k + 1)/2)` mientras más grande sea r, menos accesos van a ser necesarios (la altura del árbol queda más acotada).

Esta estructura es la más utilizada por RDBMS para implementar índices sobre tablas.

### Split

Se puede llegar a dar en una operación de *alta* en un árbol b. Cuando voy a insertar en un nodo y este ya alcanzó su load factor (máximo número de claves que puede guardar un nodo). Lo que se hace es "splittear" un maximal en dos maximales, y poner la mitad de las claves en cada una de las nuevas hojas, enviando la clave media al padre en común.
Si realizo esto y alcancé el load% del padre (solo puede pasar en carga inicial), se debe splittear el mismo. En el peor caso esto se propaga hasta la raíz del árbol b, aumentando la altura de árbol.
