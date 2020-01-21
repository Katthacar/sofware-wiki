### Pre-requisitos
- Tener un droplet con Ubuntu 18.04 x64, si no lo tienes mirar el siguiente manual: [Crear un droplet en DigitalOcean](https://github.com/doapps/software/wiki/Crear-un-droplet-en-DigitalOcean)
### Introducción
Cuando creas un droplet en DigitalOcean (DO) con Ubuntu 18.04 es recomendable realizar ciertas configuraciones iniciales por motivos de seguridad. En el presente capítulo se explicará un serie de pasos a seguir para tener un servidor configurado.
### Paso 1: Iniciar sesión como Root
Para iniciar sesión debes tener la **dirección IP** del servidor y la **contraseña** del usuario **root**, para lograrlo lo puedes hacer con el siguiente comando en tu consola.
```
$ ssh root@<IP_DEL_SERVIDOR>
```
Sí es la primera vez que ingresas la contraseña la puedes encontrar en el correo que se le mando a su email. Una vez ingresado te pedirán que cambies tu contraseña por una propia.
#### Usuario root
El usuario root es el usuario administrativo en un ambiente Linux y cuenta con todos los privilegios. No es recomendable usar a menudo el usuario root debido a que:
> "Un gran poder conlleva una gran responsabilidad".

Por ello en el siguiente paso crearemos un usuario y le enseñaremos como obtener privilegios cuando lo necesite.
### Paso 2: Crear un nuevo usuario
Una vez iniciada la sesión, vamos a crear el usuario.
Se usara como ejemplo el nombre de **ubuntu** pero usted puede poner el nombre que quiera.
```
# adduser ubuntu
```
Te pedirán la contraseña que tendrá el nuevo usuario, y unas preguntas mas sobre la información del usuario que puede dejarlo por default presionando `ENTER` en todo momento.
### Paso 3: Conseder privilegios administrativos
Ahora que tenemos nuestro usuario con privilegios basicos, aveces nos gustara hacer tareas administrativas. Para evitar tener que desconectarnos de nuestro usuario actual y conectarnos con el usuario **root**, vamos a configurar lo que es conocido como "superuser" o un usuario con privilegios root. Esto permitira que el usuario pueda realizar tareas administrativas con la palabra `sudo`.

Como **root**, ingresar el siguiente comando para darle privilegios al usuario **ubuntu**.
```
# usermod -aG sudo ubuntu
```
Ahora, usando nuestro nuevo usuario podremos hacer tareas administrativas usando el comando sudo.
### Paso 4: Configurar un Firewall básico
Ahora configuraremos un Firewall básico para proteger los puertos de nuestro servidor usando UFW.
Algunas veces, las aplicaciones que instalas registran sus perfiles con UFW despues de la instalacioón, uno que viene por default al crear un servidor con Ubuntu es el OpenSSH lo cual permite bloquear todo tipo de **conecciones excepto el de ssh**.
Para ver la lista de aplicaciones se usa el siguiente comando:
```
# ufw app list
```
```
Output
Available applications:
  OpenSSH
```
Para asegurar que nuestro servidor solo acepte conecciones SSH debemos permitir el OpenSSH con el siguiente comando:
```
# ufw allow OpenSSH
```
Despues debemos activar nuestro ufw (en caso no se encuentre activado).
```
# ufw enable
```
Digite `Y` y presione `ENTER` para finalizar el proceso. Luego podra ver el estado del ufw con el siguiente comando:
```
# ufw status
```
```
Output
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
OpenSSH (v6)               ALLOW       Anywhere (v6)
```

Si deseas eliminar alguna regla de la lista puedes usar el siguiente comando:
```
# ufw delete allow 8000
```
```
# ufw delete allow OpenSSH
```

### ¿Qué puedo hacer a partir de aquí?
Al terminar este manual ya tendrás su servidor listo para instalar cualquier aplicativo. Opcionalmente puede configurar su servidor para conectarse por medio del uso de SSH key en el [siguiente manual](https://github.com/doapps/software/wiki/Configurar-claves-SSH-en-Ubuntu-18.04), o siempre puede visitar la [página del contenido](https://github.com/doapps/software/wiki/Manuales-inicio) para mas manuales.