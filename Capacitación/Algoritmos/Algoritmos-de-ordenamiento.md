<kbd>
<img src="https://upload.wikimedia.org/wikipedia/commons/f/fe/Quicksort.gif" width="100%"/>
</kbd>
 

Los algoritmos de ordenamiento nos permite reorganizar información de una manera especial basándonos en un criterio de ordenamiento.

### ¿Por que ordenar datos?

- Es mucho mas eficiente trabajar con datos cuando la información esta ordenada.
- Reduce significativamente la complejidad de los problemas y es una técnica que reduce la complejidad de búsqueda.
 
### ¿Qué podemos ordenar?

Podemos ordenar cualquier dato que sea comparable, por ejemplo:

- Números
- Meses
- Nombres

### ¿Como ordenamos objetos?

Es decir como podemos libros, alumnos, ciudades, etc. Podemos ordenar cualquier cosa que tenga algún identificador o dato que sea comparable.

##  Selection Sort

Es un algoritmo de ordenamiento que requiere **O (n2)** operaciones para ordenar una lista de *N* elementos.

**Su funcionamiento es el siguiente:**

1.   Buscar el mínimo elemento de la lista
2.   Intercambiarlo con el primero
3.   Buscar el siguiente mínimo en el resto de la lista
3.  Intercambiarlo con el segundo

Y en general:

-   Buscar el mínimo elemento entre una posición  *i*  y el final de la lista
-   Intercambiar el mínimo con el elemento de la posición  *i*

```kotlin
fun <T:Comparable<T>>selectionsort(items:MutableList<T>):MutableList<T>{  
    if (items.isEmpty()){  
        return items  
    }  
    for (idx in 0..items.count()){  
        val array = items.subList(0,items.count()-idx)  
        val minItem = array.min()  
        val indexOfMinItem = array.indexOf(minItem)  
        if (minItem != null) {  
            items.removeAt(indexOfMinItem)  
            items.add(minItem)
        }  
    }  
    return items  
}
```

**Complejidad computacional:**
<!---Cuadratica-->
+ Mejor caso : Ω (n2)
+ Promedio : O (n2)
+ Peor de los casos : O (n2)

>Es importante recordar que la notación, ya sea O, Ω o Θ, expresa el **crecimiento asintótico de una función**, no tiene nada que ver intrínsecamente con los algoritmos en sí mismo.
Puedes encontrar mas información [aquí](https://stackoverflow.com/questions/1960424/what-is-the-difference-between-o-%ce%a9-and-%ce%98)

##  QuickSort

Es un algoritmo de clasificación eficiente  **O (N log N)** , que sirve como un método sistemático para colocar los elementos de una matriz en orden.

> La eficiencia algorítmica es una propiedad de un algoritmo que se relaciona con la cantidad de recursos computacionales utilizados por el algoritmo.
> 
> Los recursos computacionales más simples son el tiempo de cálculo , la cantidad de pasos necesarios para resolver un problema y el espacio de memoria.

**Su funcionamiento es el siguiente:**

-   Elegir un elemento del arreglo de elementos a ordenar, al que llamaremos  **pivote**.
-   Resituar los demás elementos de la lista a cada lado del pivote, de manera que a un lado queden todos los menores que él, y al otro los mayores. Los elementos iguales al pivote pueden ser colocados tanto a su derecha como a su izquierda, dependiendo de la implementación deseada. En este momento, el pivote ocupa exactamente el lugar que le corresponderá en la lista ordenada.
-   La lista queda separada en dos sublistas, una formada por los elementos a la izquierda del pivote, y otra por los elementos a su derecha.
-   Repetir este proceso de forma recursiva para cada sublista mientras éstas contengan más de un elemento. Una vez terminado este proceso todos los elementos estarán ordenados.

```kotlin
fun <T:Comparable<T>>quicksort(items:List<T>):List<T>{  
    if (items.count() < 2){  
        return items  
    }  
    val pivot = items[items.count()/2]  
    val equal = items.filter { it == pivot }  
    val less = items.filter { it < pivot }  
    val greater = items.filter { it > pivot }  
    val quick = quicksort(less) + equal + quicksort(greater)  
    return quick  
}
```

**Complejidad computacional:**

+ Mejor caso : Ω(n log(n)) <!---Logaritmica-->
+ Promedio : Θ(n log(n)) <!---casi lineal -->
+ Peor de los casos : O(n^2) <!---cuadrática-->

##  InsertionSort

Es un algoritmo de clasificación simple que construye la matriz final ordenada (o lista) un elemento a la vez. Es mucho menos eficiente en listas grandes que los algoritmos más avanzados como ***Quicksort***.

**Su funcionamiento es el siguiente:**

Este metodo funciona de la siguiente manera, toma cada elemento del arreglo y lo compara
con elementos que se encuentran en posiciones anteriores. Si resulta que el elemento con el que se está comparando es mayor que el elemento a ordenar, estos se intercambian de posición.
Si por el contrario, resulta que el elemento con el que se está comparando es menor que el elemento a ordenar, se detiene el proceso de comparación pues, se encontró que el elemento ya está
ordenado y se coloca en su posición.

```kotlin
fun <T:Comparable<T>> insertionsort(items:MutableList<T>):List<T>{
    if (items.isEmpty()){
        return items
    }
    for (count in 1..items.count() - 1){
        val item = items[count]
        var i = count
        while (i>0 && item < items[i - 1]){
            items[i] = items[i - 1]
            i -= 1
        }
        items[i] = item
    }
    return items
}
```

**Complejidad computacional:**

+ Mejor caso : Ω(n) <!---constante-->
+ Promedio : Θ(n^2) <!---cuadrática -->
+ Peor de los casos : O(n^2) <!---cuadrática-->

### :rocket:  Encuentra  [aquí](https://github.com/DavidBarbaran/sorting-algorithms)  el codigo fuente de la demo.

## Fuentes

 - [Kotlin algorithm](https://github.com/gazolla/Kotlin-Algorithm)
 - [Kotlin algorithm club](https://github.com/bmaslakov/kotlin-algorithm-club)
  - [Algorithmic efficiency](https://en.wikipedia.org/wiki/Algorithmic_efficiency)
 - [Computational resource](https://en.wikipedia.org/wiki/Computational_resource)
 - [What is the difference between O, Ω, and Θ?](https://stackoverflow.com/questions/1960424/what-is-the-difference-between-o-%ce%a9-and-%ce%98)
 -  [Big-O Cheat Sheet](http://bigocheatsheet.com/)
 - [Ordenamiento por selección](https://es.wikipedia.org/wiki/Ordenamiento_por_selecci%C3%B3n)
 - [Selection sort](https://en.wikipedia.org/wiki/Selection_sort)
 - [Quicksort (es)](https://es.wikipedia.org/wiki/Quicksort)
 - [Quicksort (en)](https://en.wikipedia.org/wiki/Quicksort)
 - [Insertion sort](https://en.wikipedia.org/wiki/Insertion_sort)