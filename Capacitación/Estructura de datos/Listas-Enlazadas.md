# Listas enlazadas
![alt text](http://codigolibre.weebly.com/uploads/5/5/8/1/55818481/1982777_orig.png)

## ¿Que son las listas enlazada?
Una lista es una secuencia de elementos dispuesto en un cierto orden, en la que cada elemento tiene como mucho un predecesor y un sucesor. El número de elementos de la lista no suele estar fijado, ni suele estar limitado por anticipado. Representaremos la estructura de datos de forma gráfica con cajas y flechas. Las cajas son los elementos y las flechas simbolizan el orden de los elementos.

![alt text](http://www.ciberaula.com/imagenes/edlista.gif)

La estructura de datos deberá permitirnos determinar cuál es el primer elemento y el último de la estructura, cuál es su predecesor y su sucesor (si existen de cualquier elemento dado). Cada uno de los elementos de información suele denominarse nodo.

La lista también puede representarse de forma simbólica escribiendo sus elementos separados por comas y encerrados entre corchetes. Por ejemplo:

["rojo","verde","azul","amarillo"]

## Tipos de listas :

1- Listas simples enlazadas:

Es una lista enlazada de nodos, donde cada nodo tiene un único campo de enlace. Una variable de referencia contiene una referencia al primer nodo, cada nodo (excepto el último) enlaza con el nodo siguiente, y el enlace del último nodo contiene NULL para indicar el final de la lista. Aunque normalmente a la variable de referencia se la suele llamar top, se le podría llamar como se desee.

![alt text](https://sites.google.com/site/programacioniiuno/_/rsrc/1472783417757/temario/unidad-3---estructuras-de-datos-comunes-y-colecciones/la-estructura-lista/lista-enlazada-append.png)

2- Listas doblemente enlazadas

Un tipo de lista enlazada más sofisticado es la lista doblemente enlazada o lista enlazadas de dos vías. Cada nodo tiene dos enlaces: uno apunta al nodo anterior, o apunta al valor NULL si es el primer nodo; y otro que apunta al nodo siguiente, o apunta al valor NULL si es el último nodo.

En algún lenguaje de muy bajo nivel, XOR-Linking ofrece una vía para implementar listas doblemente enlazadas, usando una sola palabra para ambos enlaces, aunque esta técnica no se suele utilizar.

![alt text](http://decsai.ugr.es/~jfv/ed1/tedi/cdrom/icons/lenlaz2.gif)

3- Listas enlazadas circulares

En una lista enlazada circular, el primer y el último nodo están unidos juntos. Esto se puede hacer tanto para listas enlazadas simples como para las doblemente enlazadas. Para recorrer una lista enlazada circular podemos empezar por cualquier nodo y seguir la lista en cualquier dirección hasta que se regrese hasta el nodo original. Desde otro punto de vista, las listas enlazadas circulares pueden ser vistas como listas sin comienzo ni fin. Este tipo de listas es el más usado para dirigir buffers para “ingerir” datos, y para visitar todos los nodos de una lista a partir de uno dado.

![alt text](https://upload.wikimedia.org/wikipedia/commons/d/df/Circularly-linked-list.svg)

# Fuentes :
[http://www.ciberaula.com/articulo/listas_en_java](http://www.ciberaula.com/articulo/listas_en_java)
[https://es.wikipedia.org/wiki/Lista_enlazada](https://es.wikipedia.org/wiki/Lista_enlazada)
[https://github.com/doapps/software/wiki/Buenas-pr%C3%A1cticas-al-realizar-commits](https://github.com/doapps/software/wiki/Buenas-pr%C3%A1cticas-al-realizar-commits)