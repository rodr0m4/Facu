Los métodos de ordenamiento interno se aplican a elementos que están todos en memoria, los externos a conjuntos demasiado grandes como para tenerlos en memoria.

# Heapsort

El heapsort utiliza como estructura auxiliar un árbol binario de orden parcial.

Los pasos son los siguientes:
1) Barro x niveles para obtener un vector
2) Intercambio V[1] por V[N]
3) N -= 1
4) Rearmo para que el árbol tenga orden parcial entre 1 y N
5) Si N != 1, repito el algoritmo

**Características**
* Proceso de carga de un nodo en un árbol binario tiene complejidad log₂n+1 para un elemento, por lo que, para n elementos, el mismo será de: n * log₂(n+1).
* La complejidad del orden es la misma que la carga (árbol binario), por lo que la complejidad del mismo sigue siendo n * log₂(n+1).

**Carga del AB**

Defino un AB casi completo de N nodos donde la clave de un nodo es <= a la clave de su padre (parcialmente ordenado). Luego se van insertando siguiendo la regla: "Hijo izq libre, hijo der libre, hijo izq del hermano", asi sucesivamente, barriendo por nivel. Si el nodo a ingresar es más grande que el elemento a comparar, se hace un swap (el nuevo queda como padre, el viejo padre queda como hijo).
Al insertar en el vector, se siguen unas fórmulas para saber donde hay que guardarlo:

* hijo izq(x) = ((x+1) * 2) - 1
* hijo der(x) = (x+1) * 2
* padre(x) = floor((x-1) / 2)

Ordeno totalmente el árbol, y el vector acompañante. Cuando quede todo el árbol ordenado se que el vector también lo estará.

# Quicksort

Sea x un vector y n la cantidad de posiciones.

* Elijo un elemento del mismo (en general el primero a = x[1]). Asumo que los elementos quedan repartidos de la siguiente manera, si 1 = j.
  - [1...j-1] son <= a
  - [j+1...n] son >= a

Si se cumplen esas condiciones se dice que a está ordenado, y se procede a ordenar por quicksort [1..j-1] y [j+1..n].

Debo primero ordenar el elemento a, y lo hago usando dos ptrs, `up` y `down`.

El algoritmo:

```
flag = up
while (down < up):
  if (flag == up):
    if (vec[down] < vec[up]):
      up -= 1
    else:
      swap(down, up)
      down += 1
      flag = down
  elsif (flag == down):
    if (vec[down] < vec[up]):
      down += 1
    else:
      swap(down, up)
      up -= 1
      flag = up
```

Luego de terminar de aplicar este algoritmo se que a va a estar ordenado dentro del vector, ahora solo debo ordenar utilizando el mismo algoritmo los subvectores izquierdo y derecho con respecto a a.


# Comparación entre QS y HS

El mejor caso de QS es n * log₂(n + 1) (igual que HS)
El peor caso de QS es n² (cuando el vector ya vino ordenado).

HS es consistente, su caso promedio y peor caso son iguales.

En teoría debería ser mejor HS para cualquier caso, pero QS puede ser aplicado concurrentemente.


# Árbol Binario de Búsqueda

* Todos los descendientes menores de un nodo a la izquierda, y los mayores a la derecha.
* El recorrido simétrico del mismo va a generar una lista ordenada.
* Todas las operaciones (CRUD) son de orden logarítmico promedio, lineal en worst-case

## Insersión

Inserta si la búsqueda no tiene éxito. Siempre manteniendo el orden.

## Borrado

Si no tiene hijos el nodo puedo borrarlo sin problemas. Si tiene uno o dos hijos, debo aplicar:

`Hijo izq -> padre, hijo der -> se mantiene` 

## Rotación (Balanceo)

No necesariamente tengo que balancear todo el árbol, si no que debo identificar el subárbol que esté desbalanceado, y solo balancear este.
Para balancear tomo la mediana, para que sea la nueva raiz, y aplico:
*Para desbalanceo izquierdo:*
  - padre der => hijo der
  - hijo izq => hijo izq
  - hijo der => hijo del padre der
*Para desbalanceo derecho:*
  - padre izq => hijo izq
  - hijo der => hijo der
  - hijo izq => hijo del padre izq

Algorítmicamente (para rotación hacia derecha):

```
aux = front->izq
front->izq = aux->der
aux->de = front
front = aux
```

# Árbol balanceado

`Sean x,y,z ∈ P y R(x) = {y, z} decimos que T(P, E) es balanceado, <=> ∀x se cumple que: ||R(y)| - |R(z)|| <= 1`

Se llama punto crítico al nodo a partir del cual queda desbalanceado el árbol.

## Árbol AVL

Como mantener un árbol totalmente balanceado es costoso, se inventó este tipo de árboles, también llamados balanceados en altura (La altura es la longitud de paso máxima entre un nodo y la raíz, se lo llama h(x)).

Un árbol AVL verifica `|h(y) - h(z)| <= 1`
