# Teoría de Grafos

Dado un conjunto de puntos `P` y uno de relaciones `E`, la representación gráfica es un grafo `G(P, E)`

Ejemplo:

```
Sean
P = { x, y, z }
E = { e1: (x; y), e2: (x; z), e3: (z; z) }

G(P, E) es:

|x| -e1-> |y|
    -e2-> |z|<e3>
```

**Loop:** Un arco del estilo `(x; x)`

**Minimal:** 
$$
(a \in P \land b \in P \land (b, a) \in E \implies a = b) \iff a \in minimales(G)
$$

**Maximal:**
$$
(a \in P \land b \in P \land (a, b) \in E \implies a = b) \iff a \in maximales(G)
$$

**Left:** El `Left(a)` es el conjunto de nodos desde los cuales sale un arco a `a` 

**Right:** El `Right(a)` es el conjunto de nodos hacia los cuales va un arco que sale de `a`

**In-Degree** `°L(x)°` es `|Left(x)|`

**Out-Degree** `°R(x)°` es `|Right(x)|`

**Subgrafo Parcial:** 
$$
P' = P \iff E' \in E \implies G'(P', E') es S.P de G(P, E)
$$

**Subgrafo:**
$$
P' \in P \iff E' \in E \implies G'(P', E') es Subgrafo de G(P, E)
$$

**Complejidad computacional:** Cuanto tarda un algorítmo
**Complejidad espacial:** Que tan eficiente es el uso de memoria de un algoritmo

**Paso:**
$$
\exists \delta (a, b) = { y0, y1, ..., yn }, n > 0 \\
si\ y\ solo\ si \\
a) a = y0, b = yn \\
b) y_{i-1} \ne y_i \\
c) (y_{i-1}, y_i) \in E, \forall i 1 < i < n
$$

**Longitud de un paso:** cardinalidad del mismo

*En criollo:* Conjunto de arcos que debo recorrer para ir de un nodo hacia otro. Para todo nodo existe un paso de longitud 0, que representa un arco no existente (wtf?). Un loop tiene paso 1

**Paso simple:** Se dice cuando el paso no tiene repetidos

**Ciclo:** Paso simple de longitud > 2, donde el primer y el último nodo coinciden

**Relación de paso:** Es reflexiva y transitiva. Por lo que se podría reescribir un grafo poniendo todos los pasos posibles.

**Walk:** es un paso no direccionado (no importa la dirección de la flecha)

**Ideal Izquierdo:** conjunto de nodos desde los cuales hay paso
**Ideal derecho:** conjunto de nodos hacia los cuales hay paso (nunca es vacío)

**Ideal principal:** si el ideal está compuesto por un solo elemento, se lo denomina Principal (izquierdo o derecho). En un grafo de un solo elemento, coinciden los ideales.

**Grafo básico:** Se quitan los arcos redundantes (por ejemplo los que marcan una relación de paso, arcos intermedios). Disminuye el espacio ocupado por el grafo, a cambio de aumentar el tiempo de búsqueda.

```
Un grafo acíclico G(P, E) es básico <=>

1) no tiene loops
2) ∀x, z ∈ P; ∃ |𝜹(x, z)| . 2 => (x, z) ∉ E
```

**Clausura transitiva de un grafo:** Se le agregan todos los arcos de paso, e intermedios. Mejora el tiempo de búsqueda.

### Clasifiación de grafos 
1) Lineales
2) Acíclicos
3) Irrestrictos
4) Árboles

**Grafo Lineal:** Relación de paso es total, y es básico 

## Matriz de clausura transitiva

Empiezo con la matriz de adyacencia, y realizo multiplicación booleana contra si misma, hasta llegar a una matriz idéntica a la anterior (cada multiplicación me da todos los pasos de longitud 0, 1, 2...). La ultima matriz (la que al multiplicar es igual) es la de *clausura transitiva*, y permite conocer si entre dos nodos cualesquiera existe paso.

## Warshall

**Uso del algoritmo:**
* Permite conocer la cantidad de pasos distintos de misma longitud entre dos nodos.
* Para saber la longitud de paso mínima entre dos nodos.

Es como matriz de clausura transitiva, pero con multiplicación de matrices en vez de booleana.

Completar?
