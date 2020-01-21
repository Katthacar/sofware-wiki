![Banner](http://www.devopstechlab.com/wp-content/uploads/2018/01/git-banner-1-1500x430.jpg)

## Contenidos

1.  <a  href="#introduction">¿Por qué realizar commits?</a>
2.  <a  href="#tips">Recomendaciones</a>
3.  <a  href="#basic-commands">Comandos básicos</a>
4.  <a  href="#bonus-track">Bonus track</a>

  
<a  name="introduction" />

## ¿Por qué utilizar commits?

- Para realizar un correcto control de cambios, registrando commit cada vez exista un progreso en el desarrollo
- Para que el equipo de desarrollo pueda realizar revisiones efectivas
- Para identificar los pases a producción(tags)

En DoApps tenemos un listado de buenas prácticas a considerar a la hora de realizar commits, las puedes revisar [aquí](https://github.com/doapps/git/wiki/Commits).
  
<a  name="tips" />

## Recomendaciones

Consejos puntuales a la hora de trabajar con commits:

- No finalizar los títulos con un punto
- Para identificar los lanzamientos
- Usar un modo imperativo al nombrar al commit.
- Siempre iniciar con mayúscula

Si necesitan ver los commits de forma compacta pueden usar los siguientes comandos:

```
git log --oneline
```

```
git shortlog
```

<a  name="basic-commands" />

## Comandos básicos
Cuándo el mensaje del commit no es lo suficiente para describir el motivo y los cambios realizados se puede optar por agregar una descripción al commit.

Usar el siguiente comando:

```
git commit -m ‘mensaje’ -m ‘descripcion’
```

Para listar los commits pendientes por subir:

```
git log origin/develop..develop
git log origin/master..HEAD
```

Para listar los commits ya subidos:

```
git log origin/develop
```

<a  name="bonus-track" />

## Bonus track

Si realizas cambios en la rama master y cambias de rama sin hacer commits heredas esos cambios pendientes de commitear.

Si haces un commit en cualquiera de las ramas los cambios pendientes desaparecen de todas las ramas y el commit solo le pertenece a la rama en donde se realizó el commit.
  
## Fuentes

 - [https://github.com/erlang/otp/wiki/writing-good-commit-messages](https://github.com/erlang/otp/wiki/writing-good-commit-messages)

- [https://www.atlassian.com/git/tutorials](https://www.atlassian.com/git/tutorials)

 