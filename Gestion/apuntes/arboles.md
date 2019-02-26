# Árboles

Un árbol es un grafo acíclico finito T(P, E) tq

```
1) |P| = |E| + 1 => Todo arco es desconectante.
2) T es un árbol <=> entre dos nodos cualesquiera hay un walk único.
```

**Subárbol:** Dado un árbol T, decimos que T' es un subárbol <=> T' es un subgrafo conectado (o sea es un árbol por ser parte de un árbol).

**Subárbol Principal Izquierdo:** de un nodo x es un subárbol que contiene el conjunto de nodos desde los cuales hay paso a x
**Subárbol Principal Derecho:** de un nodo x es un subárbol que contiene el conjunto de nodos hacia los cuales hay paso a x

**Árbol Principal Izquierdo:** <=> ∃ un único SPI y es todo el árbol.
**Árbol Principal Derecho:** <=> ∃ un único SPD y es todo el árbol. Es el "árbol de manual", también llamado árbol computacional.

## Características del APD

1) x es minimal, y se lo denomina *raíz* => |L(x)| = 0 (no tiene arcos que llegan hacia el).
2) ∀y ≠ x => |L(y)| = 1
3) R(x) = P
4) y es maximal y se lo denomina *hoja* => |R(x)| = 0 (no tiene arcos que salen desde el)

Análogamente se define lo contrario para el API

**Grado de un árbol:** Es el máximo grado de salida de todos los nodos del árbol. Un árbol de grado 2 es *binario*, uno de grado 3 es *ternario* y uno de grado n es *n-ario*

**Profundidad de un nodo:** Longitud del paso entre la raiz y ese nodo.

**Niveles de un árbol:** Clase de equivalencia de los nodos de la misma profundidad.

**Árbol completo:** Todos sus nodos no maximales tienen el mismo grado de salida

**Árbol lleno:** Es completo y todas sus raices tienen el mismo nivel. Su cardinalidad máxima esta dada por: `|P| = ∑ rⁱ` donde r es el grado de salida del árbol, e i es cada nivel del árbol.

## Operaciones sobre árboles

### Barridos

Orden definido en un conjunto de nodos. Aplicado sobre un APD, retorna una estructura lineal.

**Por niveles:** Se barre desde la raíz hacia todos los niveles, recorriendo cada uno en órden.

**Preorden:** Raiz - Izquierda - Derecha. Cada uno de los subárboles (y los subárboles dentro de los mismos), se barren recursivamente de la misma manera.

**Simétrico:** Izquierda - Raiz - Derecha.

**Postorden:** Izquierda - Derecha - Raiz.

### Knuth

Transforma un árbol n-ario en uno binario.
Dado un nodo, coloca como hijo izquierdo al primer elemento de su right y como hijo derecho el siguiente nodo del mismo nivel. Se dan equivalncias del tipo:

PREORDEN original === PREORDEN Knuth
POSTORDEN original === SIMÉTRICO Knuth

Estructura:

* ID_NODO
* Left_Link(v): puntero al padre de v en el árbol original
* Right_Link(v): puntero al primer hijo de v en el árbol original
* Next_Right_Link(v): puntero al primer hermano de v
