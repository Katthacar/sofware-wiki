## Estructura de datos: Arboles o Trees

### Introducción
Los arboles son definidos como un conjunto de nodos en el cual existen un nodo **raíz**  que apunta a **n** nodos que son llamados **hijos** y a su vez **sub-arboles**, por lo cual se usa mucho la recursividad.

<img src="https://i.ibb.co/ZKhB9xb/Screen-Shot-2019-01-09-at-11-24-06.png" width="500" height="300">

#### Terminologia básica

 - **Nodo raíz:** Es el nodo principal del árbol, no cuenta con un nodo padre, es decir que su padres es `null`.
 - **Sub-árbol:** Si el nodo no es el nodo raíz, entonces es un sub arboles de su nodo padre. Ejemplo: T1, T2, T3 son sub-arboles del nodo A.
 - **Nodo hoja:** Si un nodo no cuenta con hijos o descendientes, entonces es un nodo hoja.
 - **Ruta:** Una ruta es el conjunto de 'ramas' entre dos nodos. Ejemplo: La ruta de A a J es -> A, C, G y J.
 - **Nodo padre:** Es el predecesor de un nodo.
 - **Nodos hijos:** Son los nodos sucesores a un nodo.
 - **Nivel:** Cada nodo en un árbol cuenta con un nivel, el cual el nodo raíz tiene nivel 0 y sus nodos hijos son nivel 1, en pocas palabras el nivel de un nodo se da por el `nivel_padre + 1`.

Los arboles se caracterizan por la siguiente reglas:
- Uno nodo solo puede tener un nodo padre, salvo el nodo raíz.
- Un nodo puede tener cero o muchos hijos.

### Tipos de arboles
Estructura de datos abstracta (ADT), son tipos de datos que se definen por su comportamiento. Los arboles tienen muchos datos abstractos la cual se mencionaran algunas:
 - Arboles binarios
 - Arboles binarios de búsqueda (Search Binary Tree)
 - Forest
 - B - trees

## Arboles Binarios
Uno de los tipos mas populares de arboles es el árbol binario (binary trees), cuenta con las siguientes características:

- Un nodo puede tener como máximo 2 hijos.
- Se hace referencia a sus hijos como **hijo de la izquierda**  e **hijo de la derecha**

<img src="https://i.ibb.co/kK9kfZQ/Screen-Shot-2019-01-09-at-14-18-25.png" width="500" height="250">

Un árbol binario se le llama completo cuando satisface 2 propiedades: 

- Cada nodo menos los del ultimo nivel, deben estar completos (o sea tener sus dos hijos).
- Cada nodo aparece tan a la derecha como es posible.

## Recorriendo un árbol binario

Recorrer un árbol binario significa visitar cada nodo una sola vez de todo el árbol, existen diferentes algoritmos de recorrido sobre el siguiente árbol binario.

<img src="https://i.ibb.co/BKCV66Q/Screen-Shot-2019-01-09-at-14-26-15.png" width="500" height="300">

### Recorrido pre - orden
El algoritmo funciona de la siguiente manera:

- Visitar el nodo
- Recorrer el sub-árbol de la izquierda
- Recorrer el sub-árbol de la derecha

Resultado del recorrido: A - B - D - G - H - L - E - C - F -I - J - K
### Recorrido in - orden
El algoritmo funciona de la siguiente manera:

- Recorrer el sub-árbol de la izquierda
- Visitar el nodo
- Recorrer el sub-árbol de la derecha

Resultado del recorrido: G - D - H - L - B - E - A - C - I - F - K - J
### Recorrido pos - orden
El algoritmo funciona de la siguiente manera:

- Recorrer el sub-árbol de la izquierda
- Recorrer el sub-árbol de la derecha
- Visitar el nodo

Resultado del recorrido: G - L - H - D - E - B - I - K - J - F - C - A

## Arboles binarios de búsqueda
Un árbol binario de búsqueda es aquel árbol binario que cuenta con las siguientes reglas:

- El sub-árbol izquierdo de un nodo `N`, sus valores son menores que el valor de `N`.
- El sub-árbol derecho de un nodo `N`, sus valores son mayores que el valor de `N`.

<img src="https://i.ibb.co/gdGk20P/Screen-Shot-2019-01-11-at-09-52-52.png" width="500" height="300">

El árbol binario de búsqueda tiene como promedio a la hora de buscar de O(log2N), debido a que en cada paso elimina la mitad de los posibles resultados.

**Ejemplo:** Crear un árbol binario de búsqueda con los siguientes elementos: 45, 39, 56, 12, 34, 78, 32, 10, 89, 54, 67, 81.

### Operaciones

- Buscar
- Insertar
- Eliminar
- Recorridos pre/in/pos - orden

## Ultimas palabras
Se ha visto de manera básica como son los conceptos de un árbol, y se analizó el árbol binario y el árbol binario de búsqueda, los cuales son altamente usados pero se pueden encontrar muchos tipos de arboles que nacen bajo estos conceptos como:

- Arboles rojo-negro
- Arboles AVL
- Arboles B

Estos arboles cuentan con características al igual que el árbol binario de búsqueda, con el fin de optimizar algunas operaciones.

## Aplicaciones

- Los arboles son usados para implementar otro tipo de datos como: `hash tables`, `sets` y `maps`.
- Los arboles rojo-negro, se usan para el `kernel scheduling`.
- Los arboles B, se usan para almacenar estructura de arboles en los discos. Son usados para indexar grandes cantidades de datos.
- Los arboles B, también son usado en las bases de datos.
- Los arboles son usados en los sistemas de directorios de archivos.
- Los arboles también son usados para la construcción de compiladores.

## Referencias
Reema Thareja. (2014). Data Structures Using C. 2nd Edition.

