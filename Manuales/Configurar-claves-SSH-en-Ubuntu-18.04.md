### Pre-requisitos
- Tener Ubuntu 18.04 en su droplet de DigitalOcean, este [manual](https://github.com/doapps/software/wiki/Crear-un-droplet-en-DigitalOcean) les ayudara.
- Haber realizado la configuración básica para Ubuntu 18.04, en caso que no lo tenga puede revisar el siguiente [manual](https://github.com/doapps/software/wiki/Configuraci%C3%B3n-inicial-de-Ubuntu-18.04-x64).
### Introducción
SSH es un protocolo y programa que tiene como principal función el conectarse de manera **remota** a un servidor, en este caso a los droplets de DigitalOcean, este programa gestiona **claves RSA** lo cual es el tema que veremos en este manual.

Las **claves RSA** es uno de los primeros y mas utilizados sistemas de criptografia de llave publica, con esta clave que es mas conocida como **ssh-key** vamos a darle una mayor seguridad a nuestro droplet. Pero ¿cómo es esto posible?, debido a que cuenta con una llave publica que se compartira entre los servidores y una llave privada que solo tu lo tendras, esta clave reemplzara a la clave escrita que tiene cada usuario.

### Paso 1: Crear el par de claves RSA
Primero crearemos el ssh-key usando el siguiente comando, en este caso mis claves no las guardo por defecto y tengo una carpeta para las claves de mi DigitalOcean 
```
$ ssh-keygen -f ~/.ssh/digitalocean/<proyect-name>
```

Por defecto creara una clave de 2048-bit RSA, lo cual es muy seguro para la mayoria de casos.

Despues de precionar enter te preguntara por una **passphrase** la cual le da una mayor seguridad a su ssh-key, luego les mostrara un mensaje parecida a esta.

```
Output
The key fingerprint is:
SHA256:rHvdOOXPahRWCGgSXy88QpSO8Jvhef4LsPtIDaVTcbM username@host.local
The key's randomart image is:
+---[RSA 2048]----+
|      .o+o=. .   |
|    . .o+= +. .  |
|     o == E ..   |
|      +=.. oo    |
|     .==S  . .   |
|      =B.   o    |
|      +oo. *     |
|     . +o.+ +.   |
|      +o..o+.oo  |
+----[SHA256]-----+
```

Con esto tu llave privada y publica estaran guardadas en el directorio que especifico.

### Paso 2: Copiar la clave pública en el servidor Ubuntu
Para que usted pueda conectarse a su cualquier servidor, este servidor debe tener la llave publica y para ellos vamos a tener que copiarla. Para ello usaremos uso del comando **ssh-copy-id**

```
ssh-copy-id -i ~/.ssh/digitalocean/<proyect-name> <username>@<host>
```

Importante: es necesario copiar la llave en los usuarios que deseas usar como conexión.
```
ssh-copy-id -i key-file.pub ubuntu@107.210.199.114
ssh-copy-id -i key-file.pub root@107.210.199.114
```

Le pedira la clave del usuario y listo.

### Paso 3: Autentificarse en el servidor Ubuntu usando claves SSH
Para poder autenticarse se usara el archivo **config** de ssh, para tener un acceso mas facil y rapido.

Para ello debemos editar el archivo **~/.ssh/config** y agregar los puntos requeridos `Name`, `User`, `HostName`, `Port` y `IdentityFile` segun como se ve en el ejemplo.

```
# contents of $HOME/.ssh/config
# -------------------
# Service Cloud Name
# -------------------
# Host [company name] - [project name] - [deployment]
#   User          [username]
#   HostName      [151.61.61.61]
#   Port          22
#   IdentityFile  [~/.ssh/digitalocean/sample-prod]
#   (*) userpass  [userpassword]
#   (*) keypass   [keypassword]
#   (*) dbhost    [127.0.0.1]
#   (*) dbclient  [mysql]
#   (*) dbuser    [sampleuser]
#   (*) dbpass    [samplepass]
#
#   (*) these fields will be commented
```

Una vez modificado se podra acceder al cervidor por medio del siguiente comando.

```
$ ssh <name>
```
### Paso 4: Desactivar la autentificación por medio de contraseña
Ahora desactivaremos la autenticacion por medio de contraseña para que la unica forma de ingresar sea por medio del ssh-key.

una vez ingresada por medio del paso anterior vamos a modificar el archivo **config** del servidor.

```
$ sudo nano /etc/ssh/sshd_config
```

Dentro del archivo solo deves modificar la propiedad **PasswordAuthentication**, que sirve para activar o desactivar la autenticacion por medio de password, le damos no y listo.

```
...
PasswordAuthentication no
...
```

Guardas el archivo con `CRTL + X`, luego `Y` y finalmente `ENTER`. Ahora debemos actualizar los cambios en el ssh:

```
$ sudo systemctl restart ssh
```
### ¿Qué puedo hacer a partir de aquí?
Este paso fue para darle mas seguridad a tu servidor, cuentas con todo lo necesario para poder instalar cualquier aplicativo en tu servidor. Siempre puedes visitar la [página del contenido](https://github.com/doapps/software/wiki/Manuales-inicio) para mas manuales.