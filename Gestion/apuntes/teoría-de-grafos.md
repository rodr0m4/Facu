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
