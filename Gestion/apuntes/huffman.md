# Huffman

Se utiliza para reducir el espacio ocupado y la transferencia de datos. Resuelve ambiguedades que se pudiesen dar si encodeamos texto en una codificación de tamaño variable. La idea es hacer que los caracteres que aparecen con más frecuencia en un texto ocupen menos memoria que aquellos que aparecen porcas veces.

Se utiliza una tabla de frecuencias, donde se guarda cuantas veces aparece cada caracter en el texto, y un Árbol binario. La codificación está basada en código morse.

Tabla:
|Caracter|Frecuencia|Código|Bits|Total|

Donde bits es la cantidad de bits que va a utilizar, y Total = bits * frecuencia.

En el árbol binario:
1) Cada hijo izq != nil es un 0 binario.
2) Cada hijo der != nil es un 1 binario.
3) Cada hoja del árbol es un caracter.

**Aplicación del algoritmo**

1) Hallar los dos caracteres con menor frecuencia. Si tienen 0  ocurrencias se ignoran, si dos o más caracteres tienen la misma se eligen al azar.
2) Se agregan a un árbol binario (de 3), donde la frecuencia del padre es la sumatoria de la frecuencia de los mismos, y en el identificador tiene nil.
3) Se repite recursivamente este proceso hasta completar el árbol. Luego se puede completar el campo código a partir del mismo.

*Observaciones:*
  * La optimización del algorítmo consiste en reducir su tamaño, por lo que hay que evitar tener maximales.
  * No requiere utilizar un prefijo el encoding, debido a que tanto lectura como escritura se dan siguiendo el árbol (apenas se encuentra una hoja recorriendo el árbol estamos en presencia de un caracter, tanto cuando escribimos como cuando leemos).

**Codifiación y Decodificación**

Cuando lo voy a decodificar, nada más tengo una cadena de bits que llegan constantemente. Voy recorriendo uno por uno el árbol hasta llegar a un maximal (eso quiere decir que leí el caracter que está en su nodo). Así con todos los bits que me lleguen.
Para codificar, tengo que tener guardadas las direcciones de memoria de las hojas que representan a los caracteres que voy a encodear (las guardé cuando fui creando los nodos en el árbol). Recorro el árbol bottom to top siguiendo la misma regla que cuando lo cree (si tengo padre a la izquierda quiere decir que es un 1, a la derecha un 0 y asi), hasta llegar a la raiz del árbol. Eso me va a dejar una codifiación, que voy a encodear en la tabla.
