

<img src="https://i.imgur.com/1DnO5xZ.png" width="100%"/>

Una estructura lineal de datos está conformada por ninguno, uno o varios elementos que tienen una relación de adyacencia ordenada donde existe un primer elemento, seguido de un segundo elemento y así sucesivamente hasta llegar al último.

 Cada elemento de la estructura puede estar conformado por uno o varios sub-elementos o campos que pueden pertenecer a cualquier tipo de dato.

### Arreglos:
Un arreglo puede definirse como un grupo o una colección finita, homogénea y ordenada de elementos. Los arreglos pueden ser de los siguientes tipos:

**Arreglo unidimensional:**

Es un tipo de datos estructurado que está formado de una colección finita y ordenada de datos del mismo tipo. Es la estructura natural para modelar listas de elementos iguales. Están formados por un conjunto de elementos de un mismo tipo de datos que se almacenan bajo un mismo nombre, y se diferencian por la posición que tiene cada elemento dentro del arreglo de datos.

<img src="https://i.imgur.com/eqwXgyw.png" width="100%"/>

Para declarar un arreglo tiene que indicar su tipo, un nombre único y la cantidad de elementos que va a contener.

Algunos ejemplos en Java y Kotlin:

* **Java:**
```java
String[] arrayString = new String[5];
int[] arrayInt = new int[]{1, 2, 3, 4, 5, 6, 7, 8, 9, 0};
```
* **Kotlin:**
```kotlin
val arrayString = arrayOfNulls<String>(size = 10)
val arrayInt : IntArray = intArrayOf(1, 2, 3)
```

**Arreglo multidimensionales:**

Es un tipo de dato estructurado, que está compuesto por dimensiones. Para hacer referencia a cada componente del arreglo es necesario utilizar n índices, uno para cada dimensión. El término dimensión representa el número de índices utilizados para referirse a un elemento particular en el arreglo. Los arreglos de más de una dimensión se llaman arreglos multidimensionales.

<img src="https://i.imgur.com/zHoRoMf.png" width="100%"/>

Algunos ejemplos en Java y Kotlin:

* **Java:**
```java
int[][] array = {{1, 2, 3}, {4, 5, 6}};
```
* **Kotlin:**
```kotlin
val matrix = arrayOf(intArrayOf(1, 2, 3), intArrayOf(4, 5, 6))
```

**¿Que diferencia hay entre un arreglo y una lista?**

Una lista es una estructura de datos que puede contener varios tipos de datos 
mientras que un arreglo es una estructura de un unico tipo de dato.

*  Una lista tiene un tamaño dinámico, mientras que el de un arreglo es definido en su creación.
*   Una lista no puede contener datos primitivos, sólo Objetos.
*   Una lista permite comprobar que los datos que se añaden a la colección son del tipo correcto en tiempo de compilación.
*   El arreglo puede ser de varias dimensiones, la lista es unidimensional.

Algunos ejemplos en Java y Kotlin:

* **Java:**
```java
List<Object> list = new ArrayList<>();  
list.add("Jorge");  
list.add(true");
list.add(3);
```
* **Kotlin:**
```kotlin
val array = arrayListOf("Jorge", true, 3)
```
**Diccionarios:**

Un diccionario puede ser visto como una colección de **llaves**, cada una de las cuales tiene asociada un **valor**. Las llaves no están ordenadas y no hay llaves repetidas. La única manera de acceder a un valor es a través de su llave.

Algunos ejemplos en Java y Kotlin:

* **Java:**
```java
HashMap<Object, Object> hashMap = new HashMap<>();
hashMap.put(1, "Gabriela");
hashMap.put(2, true);
hashMap.put(3, 'F');
```
* **Kotlin:**

```kotlin
val map: HashMap<Int, String> = hashMapOf(1 to "x", 2 to "y", -1 to "zz")
   ```

### Fuentes:
* https://www.ecured.cu/Arreglos_(Informática)
* https://es.stackoverflow.com/questions/47520/que-diferencia-y-beneficio-tiene-un-array-contra-el-listarray
* https://www.fing.edu.uy/inco/cursos/fpr/wiki/index.php/Diccionarios