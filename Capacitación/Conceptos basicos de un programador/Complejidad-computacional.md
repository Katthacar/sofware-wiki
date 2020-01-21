![Banner](https://cdn.pbrd.co/images/HzC2ABb.png)

## Contenidos

1.  <a  href="#introduction">Complejidad computacional</a>
2.  <a  href="#clasificacion">Clasificación de problemas</a>
3.  <a  href="#ordenes">Órdenes de complejidad</a>
4.  <a  href="#conclusiones">Conclusiones</a>

  
<a  name="introduction" />

## Complejidad computacional

- Se centra en la clasificación de los problemas computacionales de acuerdo a su dificulta
- La complejidad se mide en relación al tiempo(procesamiento) y espacio(memoria).
  
<a  name="clasificacion" />

## Clasificación de problemas

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/79/Complexity_classes_es.svg/1200px-Complexity_classes_es.svg.png" width="400">

**P**
Los problemas clase P son aquellos que pueden ser abordados durante la práctica y tratados mediante el uso de una máquina determinista en tiempo **polinómico**

**NP**
problemas intratables
Esta característica lleva a un método de resolución no determinista consistente en aplicar heurísticos para obtener soluciones hipotéticas que se van desestimando (o aceptando) a ritmo polinómico.

**NP Completos**
no cuentan con un algoritmo capaz de darles solución

La clasificación clásica de los problemas en relación a su complejidad se limitaba a los tipos P y NP.

<img src="https://omicrono.elespanol.com/wp-content/uploads/2016/06/PvsNP1.jpg" width="600">

Con el pasar de los años esta clasificación se ha ampliado y podemos ver ahora clasificaciones como el NP Hard.

<img src="https://i.stack.imgur.com/coRsj.png" width="600">


Considerar lo siguiente:

- Funciones polinómicas VS exponenciales

- También pueden revisar el [test de primalidad](https://es.wikipedia.org/wiki/Test_de_primalidad_AKS).

- Computación clásica <> Computación cuántica
Recordar que la computación clásica está basada en bits cuyos estados son 0 y 1.
Sin embargo en el esquema de la computación cuántica la únidad mínima es Qubit el cual puede tener múltiples valores complejos con lo que se podría vencer la barrera de las limitaciones de procesos computacionales asociados a problemas del tipo NP.

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/f3/Blochsphere.svg/1200px-Blochsphere.svg.png" width="300">

Pueden leer más sobre computación cuántica [aquí](https://medium.com/punto-y-coma/google-vuelve-a-la-carga-ahora-la-computaci%C3%B3n-cu%C3%A1ntica-3c9897d72bdb).

<a  name="ordenes" />

## Órdenes de complejidad
Hablamos de la función O(g) para referirnos a la función que determina el orden de complejidad de un determinando algoritmo.

En concreto O(g) será una función que estima la tasa de crecimiento asociada al número de operaciones que son necesarias realizar en un algoritmo determinado.

<img src="https://cdn-images-1.medium.com/max/1200/1*lhooB5BL6PBNBWrgLW7nPA.png" width=400>
---

Los órdenes de complejidad más conocidos se presentan en la siguiente tabla:

Orden |	Nombre
---|---
O(1) |	constante
O(log n) |	logarítmica
O(n) |	lineal
O(n log n)	| casi lineal
O(n²) | 	cuadrática
O(n³) |	cúbica
O(a^n) |	exponencial


#### Ejemplo de función con complejidad lines O(n)
Imaginemos que función suma(n) es la suma de los números de 1 hasta n. 

Por ejemplo, suma(5)  ==  15


    suma :: Integer -> Integer

    suma 0 = 0

    suma n = n + suma (n-1) 


El tiempo necesario para calcular (suma n) para n en [1000,2000..8000] se recoge en la siguiente tabla

n	|segs
--------|----
1000	|0.02
2000	|0.03
3000	|0.04
4000	|0.04
5000	|0.05
6000	|0.06
7000	|0.07
8000	|0.08

En la tabla se observa que hay una relación lineal entre n y el tiempo necesario para calcular (suma n):

    tiempo(suma n) ≈ n * 0.00001

Las ecuaciones para calcular T(n) son

    T(1)   = 1

    T(n+1) = 1 + T(n)

Demostración de que suma ∈ O(n) (es decir, es de coste lineal)

Basta comprobar que T(n) = n cumple las ecuaciones del coste de la función suma.

    T(1)   = 1       [por definición de T]

    T(n+1) = 1+T(n)  [por definición de T]

           = 1+n     [por hipótesis de inducción]
       
           = n+1     [por álgebra]

<a  name="conclusion" />

## Conclusiones
Se entiende que la complejidad de un problema está directamente relacionado a la cantidad de recursos computacionales que requiere para dicho problema para ser resuelto.
Es importante tener claro que una función exponencial representa el crecimiento de la demanda de tiempo y espacio que necesita el problema para ser resuelto lo que representa una situación poco favorable, por el contrario una función logarítmica, lineal o similares representa un crecimiento dentro de los parámetros normales.



## Fuentes
- [Análisis de complejidad](https://www.cs.us.es/~jalonso/cursos/i1m/temas/tema-28.html#definici%C3%B3n-de-og)
- [Complejidad de problemas](https://pjflores1987.wordpress.com/2012/06/20/complejidad-computacional/)



## Fuentes recomendadas para siguiente clase
- https://es.slideshare.net/joemmanuel/complejidad-computacional
- https://elisa.dyndns-web.com/teaching/aa/pdf/aa.pdf
