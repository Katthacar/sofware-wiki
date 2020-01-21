Dado que Heroku no alberga sitios web estáticos lo que podemos hacer es crear una aplicación PHP que cargue los archivos html.

## Requisitos

- Se recomienda tener los archivos html en la raíz del proyecto y probar previamente si todos los archivos css, js o assets están correctamente direccionados.
- Se recomienda no tener un archivo index.html porque eventualmente se creará un archivo index.php
- Se recomienda tener instalado **[Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli)** y configurado con sus credenciales
- Tener una carpeta con el proyecto.


## Proceso de despliegue
- Agregar el archivo *composer.json* en la raíz del proyecto.
- Agregar el archivo *index.php* en la raíz del proyecto
- Identifica tu archivo principal el cual se lanzará al cargar la url, en este caso será *home.html*
- En el archivo *index.php*, agrega la siguiente línea: `<?php include_once("home.html"); ?>`
- En el archivo *composer.json*, agrega la siguiente línea: `{}`
- Ubícate dentro de la carpeta del proyecto
- Inicia sesión con tu cuenta de heroku usado el CLI con el siguiente comando.

      $ heroku login

- En caso no uses git en ese proyecto debes ejecutar el siguiente comando:
      
      $ git init

caso contrario omite esto.

- Configuramos el repositorio remoto de heroku con el siguiente comando:
    
      $ heroku git:remote -a app-name

Debes reemplazar *app-name* por el nombre que heroku le haya asignado a tu proyecto.

- Ahora ejecuta el comando de git para agregar y empaquetar cambios.
      
      $ git add .
      $ git commit -m "new changes"

- Ahora subiremos los cambios a heroku y se realizará el despliegue automático:
      
      $ git push heroku master

- Visitamos la url proporcionada por Heroku y listo¡

### Autor: 
### [Jonathan Nolasco](https://github.com/jnolascob) | **Backend Developer** :octocat: 