# Pfaltz

```
Dado G(P, E), G es bipartito si:
* P = Q∪R
* Q∩R = ∅
* ∀(x, y)∈E: (x∈Q ∧ y∈R)∨(x∈R ∧ y∈Q)
```

## Representación algebraica

Pfaltz pasa de un G(P, E) a un G'(P', E'), haciendo que cada elemento de E pase a ser parte de P'. E' va a tener dos miembros por cada miembro de E (uno por saliente, otro por entrante), y se agregan a P' nodos como (x, y) donde x e y ∈ P.

## Representación computacional

Se tienen dos listas enlazadas (una de nodos y otra de arcos), por lo que solo ocupa memoria cuando realmente se necesita.

---

Nodo:

ID: identificador único.
fp 1..n: funciones de asignación al nodo.
LEDGE: puntero al primer Arco que llega al nodo (por orden de carga).
REDGE: puntero al primer Arco que sale del nodo.
NEXT: puntero al próximo Nodo.

---

Arco:

ID: identificador único.
ge 1..n: funciones de asignación al arco.
LPOINT: puntero al Nodo de la cual parte este arco.
RPOINT: puntero al Nodo al cual llega este arco.
LLINK: puntero al próximo Arco que comparte RPOINT.
RLINK: puntero al próximo Arco que comparte LPOINT.
NEXT: Puntero al próximo Arco.

"Los arcos entrantes siempre por izquierda, los salientes siempre por derecha".

Mientras más grande es el grafo este método es menos eficiente
