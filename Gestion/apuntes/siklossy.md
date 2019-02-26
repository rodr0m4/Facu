# Siklóssy

Es una lista doblemente enlazada, pero en vez de gastar espacio en dos punteros por nodo, usamos ⊕. Para acceder al próximo nodo, tengo que hacer XOR entre la dirección lógica del nodo anterior y el actual.
La dirección lógica (y física) del inicio y fin es *NULL*. Siempre tengo que tener guardado (para recorrer o insertar) el nodo anterior al actual.
