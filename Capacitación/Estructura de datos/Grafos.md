<img src="https://labs.vmware.com/wp-content/uploads/2013/06/VMW-DGRM-CRITICALITY-PATTERNS-IN-DIRECTED-GRAPH-102.png" width="400">

## ¿Qué es? 
Una estructura de datos abstracta.
Recordar que el concepto de grafos viene de las matemáticas.

#### ¿Un árbol es un grafo?

Un árbol es un tipo de grafo simple, conexo y sin ciclos.

## ¿Cuál es la importancia de los grafos?
A diferencia de los árboles, los grafos son una estructura de datos más flexible.
Tiene multiples aplicaciones a problemas computacionales y reales:

- Mapas:
para representar las rutas y mapear el congestionamiento.

- Redes sociales:
para manejar la relación de amistad entre personas y la recomendación de nuevos amigos.

- Base de datos NoSQL:
para aplicaciones donde la data se tenga que almacenar bajo el concepto de grafos existen soluciones como https://neo4j.com/ no confundir con graphQL.

- (*)IA: para representar las redes neuronales.


## Terminología

- **Vértice**: es la unidad fundamental del grafo, también llamado *nodo*.
- **Aristas**: es la relación entre vértices, también llamado *arcos* pueden ser unidireccionales o bidireccionales.
- **Ponderación**: es el valor asociado a una arista, generalmente es el coste de ir de un vértice a otro.

#### Casos particulares

- **Bucle**: una arista que relaciona el nodo consigo mismo.
- **Aristas paralelas**: son aristas que relacionan el mismo par de vértices.

## Tipos de grafos

**No dirigido**

Las aristas no tienen dirección definida.

**Dirigido**

Las aristas o arcos tienen dirección, es decir tienen origen y destino. su representación es en forma de flecha.

**Mixtos**

Son grafos que tienen aristas dirigidas y no dirigidas.

## Representación de grafos
Hay 2 formas conocidas para representar grafos:

- Usando matriz de adyacencia
- Usando listas de adyacencia


## Matriz de adyacencia
<img src="https://upload.wikimedia.org/wikipedia/commons/f/f9/Matriz_de_adyacencia.jpg" width="400">


Una forma de implementar un grafo es haciendo uso de matrices bidimensionales.
Si construimos la matriz de adyacencia podemos tener el grado de los vértices a manera sencilla.

Problema:
<img src="https://i.ibb.co/WP8jV4G/Screen-Shot-2019-01-17-at-4-01-15-PM.png" width="500">

Solución:
<img src="https://i.ibb.co/GpFMcVk/Screen-Shot-2019-01-17-at-4-01-56-PM.png" width="500">

## Lista de adyacencia
<img src="https://upload.wikimedia.org/wikipedia/commons/6/6f/Listas_de_adyacencia.jpg" width="500">

Es una representación más eficiente si hablamos de espacio.
También nos permite listar las conexiones de vértices de manera directa.


## Herramientas online para practicar
https://visualgo.net/el/graphds


## Implementación y métodos

- Grafo()
- agregarVertice()
- agregarArista()

## Demo

    from vertice import Vertice
    class Grafo:
    def __init__(self):
        self.listaVertices = {}
        self.numVertices = 0

    def agregarVertice(self, clave):
        self.numVertices = self.numVertices + 1
        nuevoVertice = Vertice(clave)
        self.listaVertices[clave] = nuevoVertice
        return nuevoVertice

    def obtenerVertice(self, n):
        if n in self.listaVertices:
            return self.listaVertices[n]
        else:
            return None

    def __contains__(self, n):
        return n in self.listaVertices

    def agregarArista(self, de, a, costo=0):
        if de not in self.listaVertices:
            nuevoVertice = self.agregarVertice(de)
        if a not in self.listaVertices:
            nuevoVertice = self.agregarVertice(a)
        self.listaVertices[de].agregarVecino(self.listaVertices[a], costo)

    def obtenerVertices(self):
        return self.listaVertices.keys()
    
    def __iter__(self):
        return iter(self.listaVertices.values())

Demo completo aquí:
https://gist.github.com/jnolascob/d63e31da2ff65f1404ed1a507eabc0f1


## Fuentes
- http://interactivepython.org/runestone/static/pythoned/Graphs/Objetivos.html
- http://index-of.es/Miscellanous/Data%20Structures%20Using%20C,%202nd%20edition.pdf
- https://medium.com/@matematicasdiscretaslibro/cap%C3%ADtulo-11-teoria-de-grafos-3b00228dd81c