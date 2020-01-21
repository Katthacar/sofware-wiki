<img src="https://i.imgur.com/Esvi1F5.png" width="100%"/>

## Descripción
Koin es un framework de inyección de dependencia, según el paradigma de inyección de dependencias señala que en lugar de que cada clase sea responsable de buscar sus dependencias, otra entidad será la encargada de proporcionarlas.

## Para que se uso

Para conseguir un código de calidad debemos seguir los principios [SOLID](https://en.wikipedia.org/wiki/SOLID_(object-oriented_design)). Entre ellos el primero, **"Single responsability"**, consiste en que cada elemento de nuestro código, sea una clase o un método, se encargue de una sola cosa y el quinto **"Dependency inversion"**, que permite que nuestras clases no dependan de los colaboradores sino de abstracciones de estos.
En el caso de Android según los principios **SOLID**, una Actividad, un presentador o cualquier otra clase sobre la cual trabajemos no debería ser la encargada de instanciar las entidades que trabajan sobre ella misma.

**Koin** se utilizo con este fín, ya que esta biblioteca se encargue de ello, obteniendo así una mejor calidad de código y cumpliendo el primero y el quinto de los principios **SOLID**.

#### Puedes encontrar una guía de cómo implementar ***Koin*** en tu proyecto [aquí](https://github.com/doapps/software/wiki/C%C3%B3mo-implementar-Koin-en-tu-proyecto-de-Android-X).

## Sitios oficiales

- :globe_with_meridians: [Pagina Web](https://insert-koin.io/)
- :octocat: [Github](https://github.com/InsertKoinIO/koin)
- :open_file_folder: [Documentación](https://insert-koin.io/docs/1.0/getting-started/introduction/)
- :pushpin: [Ejemplos](https://github.com/Ekito/koin-samples)