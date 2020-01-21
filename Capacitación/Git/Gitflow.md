
<img src="https://wac-cdn.atlassian.com/dam/jcr:61ccc620-5249-4338-be66-94d563f2843c/05%20(2).svg?cdnVersion=lf">

## ¿Que es Gitflow?
Gitflow es un flujo de trabajo de basado en git que fue publicado y popularizado por Vincent Driessen. 
El flujo de trabajo de Gitflow define un modelo de ramificación estricto diseñado en torno a la versión del proyecto. Esto proporciona un marco robusto para la gestión de proyectos grandes.

El proyecto original de Vincent Driessen pueden encontrarlo [aquí](https://github.com/nvie/gitflow), sin embargo no viene recibiendo mantenimiento desde el 2011.

Una alternativa igual de buena es el proyecto de Peter van der Does, que pueden encontrarlo [aquí](https://github.com/petervanderdoes/gitflow-avh) que hasta el 2019 vienen recibiendo mejoras y actualizaciones.

## ¿Porque usar Gitflow?

Por los siguientes motivos:

1. Desarrollo Paralelo
2. Colaboración
3. Área de puesta en escena de la versión
4. Soporte para reparaciones de emergencia

## Como usar GitFlow paso a paso

### 1. Instalar Gitflow
Para instalar gitflow en mac usar el siguiente comando:

- En macOS
```
brew install git-flow-avh
```

- En Linux
```
apt-get install git-flow
```

- En Windows revisar [aquí](https://github.com/petervanderdoes/gitflow-avh/wiki/Installing-on-Windows)

Para verificar que ya tienes git-flow instalado puedes verificar la versión instalada con el siguiente  comando:
`git-flow version`

### 2. Inicializar Gitflow
Una vez situado en la carpeta de tu proyecto puedes iniciar usando este comando:
```
git flow init
```
A continuación se mostrará un mensaje donde te preguntará cuales serán los nombres de las ramas **develop**, **feature**, **release**, **hotfix** y **support**, en nuestro caso le daremos tecla enter consecutivamente para dejar el nombre de las ramas por defecto.

Una vez inicializado git flow te posicionará automáticamente en la rama **develop** y a partir de aquí ya puedes crear tus features para trabajar.

<img src="https://wac-cdn.atlassian.com/dam/jcr:2bef0bef-22bc-4485-94b9-a9422f70f11c/02%20(2).svg?cdnVersion=lf">

### 3. Manejo de features

Un feature puede estar asociado a alguna funcionalidad que definas y que estés dispuesto de desarrollar hasta completarlo en un corto plazo.

Comando para crear un feature:
```
git flow feature start <name>
```

Una vez creado el feature ya puedes codificar y generar commits a medida que desarrollas.

Recuerda que todos los commits se encuentra en tu ambiente local.

Cuando finalices el desarrollo de tu feature ya puedes finalizarlo con el siguiente comando:
```
git flow feature finish <name>
```

**Ojo:** Si el feature toma más tiempo y deseas seguir desarrollando desde otra pc o deseas que alguien continue con tu feature tienes la opción de publicar tu feature de forma remota:

Pushear tus cambios al repositorio remoto:
```
git flow feature publish <name>
```

Pullear tus cambios desde el repositorio remoto:
```
git flow feature pull <remote> <name>
```
<img src="https://wac-cdn.atlassian.com/dam/jcr:b5259cce-6245-49f2-b89b-9871f9ee3fa4/03%20(2).svg?cdnVersion=lf">

### 4. Publicar un release

Cuando los features que comprenden un entregable están completados ya estamos listo para una versión estable que puede ser desplegada o publicada.
Ubícate en la rama **develop** y crear un **release**.

Comando para crear un release:
```
git flow release start <release>
```

> "<"release">" = v1.0.0


**Ojo**: Si el release necesita revisión o alguna integración previa y se trabajará en remoto puedes usar el comando
```
git flow release publish <release>
```

Si estas listo para publicar el realease:
```
git flow release finish <release>
```
Este comando hace un merge de la rama **develop** en **master** y vuelve a **develop** ya actualizado y elimina la rama **release** creada de forma temporal.


Para finalizar la publicación:
```
git push origin --all --follow-tags
```
Este comando actualizará las ramas **master** y **develop** en el repositorio remoto y además creará el tag *v1.0.0* en el repositorio remoto.

<img src="https://wac-cdn.atlassian.com/dam/jcr:a9cea7b7-23c3-41a7-a4e0-affa053d9ea7/04%20(1).svg?cdnVersion=lf">

### Bonus 
Si deseas más detalles del uso de Gitflow puedes revisar este video.
[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/BYrt6luynCI/0.jpg)](https://www.youtube.com/watch?v=BYrt6luynCI)

### Problemas
Si tienes problemas con vim o ves un mensaje similar a este:
`git-flow hotfix finish list-description-update
error: There was a problem with the editor 'vi'.
Please supply the message using either -m or -F option.
Fatal: Tagging failed. Please run finish again to retry.`

Puedes revisar aquí:
https://github.com/petervanderdoes/gitflow-avh/issues/293

# Fuentes :
* [https://nvie.com/posts/a-successful-git-branching-model/](https://nvie.com/posts/a-successful-git-branching-model/)
* [https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
* [https://datasift.github.io/gitflow/IntroducingGitFlow.html](https://datasift.github.io/gitflow/IntroducingGitFlow.html)
* [https://github.com/doapps/software/wiki/Buenas-pr%C3%A1cticas-al-realizar-commits](https://github.com/doapps/software/wiki/Buenas-pr%C3%A1cticas-al-realizar-commits)
* [https://danielkummer.github.io/git-flow-cheatsheet/](https://danielkummer.github.io/git-flow-cheatsheet/)
* [https://www.youtube.com/watch?v=BYrt6luynCI](https://www.youtube.com/watch?v=BYrt6luynCI)