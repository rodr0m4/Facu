# Sort topológico

Se utiliza en gráficos tipo PERT, donde es importante identificar períodos de tiempo y cantidades máximas/mínimas de recursos. Convierte un conjunto de precedencias en una lista lineal simple, dentro de la cual ningun elemento posterior precede a un elemento anterior.

```
     |b|--------------|e|->|h|<--|g|
      |-------------|      |i|<---|
          |------->|f|
|a|->|c|--||--------|
   ->|d|---|
```

S1: `|a|->|c|->|b|->|d|->|f|->|g|->|i|->|e|->|h|`

S2: `|b|->|e|->|a|->|d|->|g|->|c|->|f|->|h|->|i|`

Donde G es acíclico y S1 y S2 son sort topológico de G.

```
Dado un grafo finito G=(P, E), 
* Existe sort topológico S <=> G es acíclico
* S es único <=> E es una relación de orden total (S es el grafo básico de G)
```

## Procedimiento

Como G es acíclico => existe un minimal x1. Como `|L(x1)| = 0`, ingresa en la secuencia de la estructura de salida. Apenas se agrega se borra x1 de G, junto con todos sus arcos salientes (G1 sigue siendo acíclico). De esta manera G1 tiene al menos un minimal (x2), puede haber varios minimales, de los cuales se elegirá uno de manera arbitraria. Se repite el proceso hasta procesar todo el grafo.

## Implementación

Se podría utilizar la matriz de adyacencia, pero la misma no es adecuada para solucionar problemas de actualización dinámica, ya que requiere conocer por antelación el tamaño del grafo, por eso recurrimos a listas enlazadas. La que se suele usar es Pfaltz (permite guardar información de nodos y arcos en dos estructuras separadas). Se toman los minimales sin dependencias entre ellos (los que "pueden ser ejecutados en paralelo"), la menor cantidad de recursos en ese período para cada "step" es la máxima cantidad de recursos para ese step ("para 3 tareas paralelizables, las 3 van a tardar tanto como la más lenta").
