# Algoritmos de búsqueda

Un **algoritmo de búsqueda es** aquel que está diseñado para localizar un elemento con ciertas propiedades dentro de una estructura de datos; por ejemplo, ubicar el registro correspondiente a cierta persona en una base de datos.

# Búsqueda secuencial o lineal

Con la búsqueda lineal, iteramos sobre todos los objetos en nuestro arreglo  y comparamos cada uno con el objeto que estamos buscando. Si los dos objetos son iguales, detendremos y devolveremos el índice de la posición actual del arreglo. De lo contrario, continuamos buscando el siguiente objeto siempre que tengamos objetos en el arreglo.
El mejor caso es cuándo el valor es igual al primer elemento de la lista, en este caso sólo se necesita una comparación.
El peor caso es cuando el valor no esta en la lista (o se encuentra al final de la lista), en este caso se necesitan n comparaciones y podríamos no obtener nada.

```swift
let arregloStr = ["Zacarias","Aldo", "Alberto", "Bryan", "Maria"]
func busquedaLineal<T: Equatable>(arreglo: [T], _ elemento: T) -> Int {
	for (index, item) in arreglo.enumerated() where item == elemento {
		return index
	}
	return  -1
}
print("El elemento ha sido encontrado en la posición: \(busquedaLineal(arreglo: arregloStr, "Bryan"))")
```
**Complejidad**
>Peor de los casos O(n)  
> Mejor de los casos O(1)   
> Caso promedio O(n)

# Búsqueda Binaria
**Divide y conquistarás**  

La búsqueda binaria funciona en arreglos ordenados. La búsqueda binaria comienza por comparar el elemento del medio del arreglo con el valor buscado. Si el valor buscado es igual al elemento del medio, su posición en el arreglo es retornada. Si el valor buscado es menor o mayor que el elemento del medio, la búsqueda continua en la primera o segunda mitad, respectivamente, dejando la otra mitad fuera de consideración.
	
Para una matriz de tamaño n, el rendimiento no es O (n) como en la búsqueda lineal, sino solo O (log n). Para poner eso en perspectiva, la búsqueda binaria en una matriz con 1,000,000 de elementos solo toma unos 20 pasos para encontrar lo que está buscando, porque log_2 (1,000,000) = 19.9.

>Precondición -> El arreglo debe estar ordenado

![alt text](http://1.bp.blogspot.com/-qntEO_UbhX0/TgAaCk_rBzI/AAAAAAAAASo/G32GKjR3IgA/s1600/Ejemplo+B%25C3%25BAsqueda+Binaria.JPG)

**Búsqueda binaria recursiva**

```swift
func busquedaBinariaRecursiva<T: Comparable>(arreglo: [T], elemento: T, rango: Range<Int>)->Int? {
	if rango.lowerBound > rango.upperBound {
	//No se ha encontrado el elemento dentro del arreglo
	return nil
	}else {
		let indexMedio = (rango.lowerBound + rango.upperBound) / 2
		if arreglo[indexMedio] > elemento {
		return busquedaBinariaRecursiva(arreglo: arreglo, elemento: elemento, rango: 	rango.lowerBound..<indexMedio)
		}else if arreglo[indexMedio] < elemento {
		return busquedaBinariaRecursiva(arreglo: arreglo, elemento: elemento, rango: indexMedio + 1 ..< rango.upperBound)
		}else {
		return indexMedio
		}
	}
}
print(busquedaBinariaRecursiva(arreglo: arregloStr, elemento: "Bryan", rango: 0..<arregloStr.count)!)
```

**Búsqueda binaria iterativa**

```swift
func busquedaBinariaIterativa<T: Comparable>(arreglo : [T], elemento: T) -> Int? {
var minimo = 0
var maximo = arreglo.count
	while minimo < maximo {
	//calculamos el indice medio del arreglo
	let indiceMedio = (maximo + minimo) / 2
		if arreglo[indiceMedio] == elemento {
		return indiceMedio
		} else if arreglo[indiceMedio] < elemento {
		//usaremos la segunda mitad del arreglo
		minimo = indiceMedio + 1
		} else {
		//IF arreglo[indiceMedio] > elemento
		//usaremos la primera mitad del arreglo
		maximo = indiceMedio - 1
		}
	}
	return  nil
}
print(busquedaBinariaIterativa(arreglo: arregloStr, elemento: "Bryan")!)
```
**Complejidad**
>Peor de los casos O(log n)  
>Mejor de los casos O(1)   
> Caso promedio O(log n)


# Fuentes

https://www.taringa.net/Pie_Grande47/busqueda-binaria-y-busqueda-secuencial-mas-claro-echale-agua_160t25
https://github.com/raywenderlich/swift-algorithm-club/tree/master/Linear%20Search
https://github.com/raywenderlich/swift-algorithm-club/tree/master/Binary%20Search
https://en.wikipedia.org/wiki/Binary_search_algorithm
