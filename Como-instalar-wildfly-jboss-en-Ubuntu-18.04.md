# ¿Qué es Wildfly(JBoss)?
Wildfly antes conocido como JBoss es un potente servidor de aplicaciones Java open source desarrollado por RedHat. Tiene soporte para:
- Servlet 3.0
- JSF
- Java Server Faces
- EJB
- JPA
- CDI
- Bean Validation
- Entre otros.

Más documentación aquí: https://docs.jboss.org/author/display/AS71/Documentation

# Instalación:

### Instalar Java
Verificar si ya lo tienes instalado con el siguiente comando
```
java --version
```

Caso contrario instalarlo con el siguiente comando:
```
sudo apt-get install default-jdk -y
```
### Instalar Wildfly

Primero ubicarse en la carpeta **opt**

```
cd /opt
```

Luego procedemos a descargar la última versión de Wildfly

```
wget http://download.jboss.org/wildfly/14.0.1.Final/wildfly-14.0.1.Final.tar.gz
```

Descomprimimos el archivo descargado

```
tar -xvzf wildfly-14.0.1.Final.tar.gz
```

y lo movemos a una carpeta nueva llamada **wildfly**

```
sudo mv wildfly-14.0.1.Final wildfly
```

### Crear usuario de acceso

Para ingresar a la consola de administración de wildfly necesitaremos un usuario, usar este comando para crear dicho usuario:

```
sudo /opt/wildfly/bin/add-user.sh
```

Selecciona la opción a) e ingresa el usuario y contraseña deseado.

### Inicializar Wildfly
Primero debes ubicarte en la siguiente carpeta: `/opt/wildfly/bin` y luego ejecutar este comando para iniciar la instancia de *Wildfly*

```
./standalone.sh -Djboss.bind.address=yourserverip -Djboss.bind.address.management=yourserverip&
```

### Inicializar Wildfly con todos los privilegios
En caso necesites iniciar una instancia dde Wildfly con todos los privilegios disponibles debes ejecutar el siguiente comando:
```
./standalone.sh -c standalone-full.xml -Djboss.bind.address=yourserverip -Djboss.bind.address.management=yourserverip&
```
### Acceder a la consola de administración

Una vez ejecutado Wildfly saldrá un mensaje en la terminal indicando que se inicializó con éxito y te indicará en que puerto se encuentra corriendo el panel de administración.
Generalmente usa el puerto *9990* si ese es el caso solo necesita acceder a la siguiente ruta en cualquier navegador:

http://yourserverip:9990/

![](https://user-images.githubusercontent.com/3833940/53831180-34f74800-3f52-11e9-9e31-a4a89ba065a2.png)

Te solicitará el usuario y contraseña antes de monstrarte el panel.

![](https://user-images.githubusercontent.com/3833940/53831360-a800be80-3f52-11e9-932c-a35607de33f7.png)

### Detener Wildfly

Primero debes ubicarte en la siguiente carpeta: `/opt/wildfly/bin` y luego ejecutar el siguiente comando:

```
./jboss-cli.sh --connect --controller=yourserverip:9990 command=:shutdown
```

### Importante

Para acceder al panel de Wildfly con normalidad debes asegurarte de tener el puerto 9990 habilitado, de igual manera el 8080 si correr tu aplicación java en dicho puerto.

Para ver los puertos disponibles:

```
sudo ufw status
```

Para habilitar un puerto:

```
sudo ufw allow 9990
```

#### Fuentes:
- https://www.digitalocean.com/community/tutorials/how-to-install-jboss-on-ubuntu-12-10-64bit
- https://www.howtoforge.com/tutorial/ubuntu-wildfly-jboss-installation/


#### Pendientes:
- Subir imágenes de la terminal que sirva como guía.

### Autor: 
### [Jonathan Nolasco](https://github.com/jnolascob) | **Backend Developer** :octocat: 