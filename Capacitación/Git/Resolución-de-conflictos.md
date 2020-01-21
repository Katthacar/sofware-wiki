<img src="http://www.devopstechlab.com/wp-content/uploads/2018/01/git-banner-1-1500x430.jpg" width="100%">

### 1. git reset
Según la documentación, reestablece el HEAD actual al estado especificado:

**Conceptos:**
HEAD: puntero , que le dice en qué COMMIT está trabajando.

**Modos:**
hard: Lo que realiza es Deshacer los cambios y volver al estado anterior
```bash
git reset --hard "<commit>"
```
soft: combinar una serie de confirmaciones locales
```bash
git reset --soft "<commit>"
```
<img src="https://wac-cdn.atlassian.com/dam/jcr:5c4cb0f2-856c-4d39-b014-9340ef1d05e4/hero.svg?cdnVersion=ji" width="450">

:point_right: Puedes obtener información de `git reset` a detalle [aquí](https://www.atlassian.com/git/tutorials/undoing-changes/git-reset).

### 2. git fetch
Según la documentación, descarga objetos y referencias desde otro repositorio.

Cuando haces un git fetch, se van a descargar los cambios
de tu repositorio remoto(en el caso de que haya) en una
carpeta que se llama origin/master, que es una carpeta
oculta. Para incluir los cambios a tu rama local necesitas
fusionar master con origin/master.
```bash
git fetch origin master
```
<img src="https://i.stack.imgur.com/zUInQ.png" width="350">

:point_right: Puedes obtener información de `git fetch` a detalle [aquí](https://www.atlassian.com/git/tutorials/undoing-changes/git-reset).

### 3. git rebase
Según la documentación, vuelve a aplicar confirmaciones en la parte superior de otro consejo básico.

Resuelve conflictos de commits que no aportan nada.
```bash
git rebase <branch_name>
```
:point_right: Puedes obtener información de `git rebase` a detalle [aquí](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase).

### 4. git stash
Según la documentación, oculta los cambios en un directorio de trabajo sucio.

Guarda las modificaciones locales en temporal y vuelve el directorio de trabajo a un estado inicial (como si no se hubiese hecho ningún cambio en la rama).
```bash
git stash
```
Si no desea aplicar los cambios y regresar a los cambios de su ultimo commit puede usar `git stash pop` o si desea aplicar los cambios `git stash apply` y para visualizar la lista de sus stash puede usar `git stash list`.

:point_right: Puedes obtener información de `git stash` a detalle [aquí](https://frontendlabs.io/940--la-importancia-del-comando-git-stash-en-un-proyecto)

**Para eliminar ramas**
 - Locales
 ```bash
git branch -d feature/branch_name
```
 - Remotas
 ```bash
git push origin --delete feature/branch_name
```
git branch --delete feature/maquetado [local]
git push --delete origin develop [remota]

### :rocket: Encuentra [aquí](https://drive.google.com/open?id=1FfxCgmx0-emY7NTJFafwX2LP9OYY__85) la PPT de la presentación. 