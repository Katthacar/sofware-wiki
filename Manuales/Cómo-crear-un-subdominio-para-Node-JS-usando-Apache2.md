Muchos servidores usan Apache2 para realizar el manejo de sus dominios y sub dominios, hay ocaciones en la que es necesario crear un sub dominio en donde corra tu app en [Node.js](https://nodejs.org/en/), en este manual vamos a ver paso a paso como lograrlo.

### Requisitos

* Tener Apache2 instalado en tu servidor o maquina local, que tenga como sistema operativo Ubuntu.
* Contar con un hosting y DNS apuntando a tu servidor.
* Tener un usuario con privilegios `sudo` (no tiene que ser el usuario 'root').

### Paso 1: Entender como funciona Apache2
Apache2 es un servidor web que te permite crear diferentes virtualHosts en las cuales puedes agregarlos diferentes dominios o sub dominios.
Para crear un virtualHost necesitas crear un archivo `.conf` que cuente con la configuración necesario para que apache la entienda y cree el sub dominio, lo cual veremos a continuación.

### Paso 2: Instalar modulos de Apache2
Para el ejemplo usaremos el dominio `myweb.com` y deseamos crear un sub dominio  `api.myweb.com` para alojar nuestro backend que fue desarrollado usando Node.js y se encuentra corriendo en el puerto 8000.

Para lograr el proxy es necesario agregar algunos módulos a Apache2.

Vamos a instalar los siguientes módulos

* SSL
* Proxy
* Proxy Balancer
* Proxy HTTP

En la consola de su servidor digitar

```
sudo a2enmod ssl
sudo a2enmod proxy
sudo a2enmod proxy_balancer
sudo a2enmod proxy_http
```

### Paso 3: Crear tu archivo .conf
Crear el archivo `api.myweb.com.conf` en la carpeta `/etc/apache2/sites-available/`
```
$ sudo nano /etc/apache2/sites-available/api.myweb.com.conf
```
Dentro del archivo vamos a digitar lo siguiente:

```
<VirtualHost *:80>
        ServerName api.myweb.com
        ServerAdmin api@admin.com

        # setup the proxy
         <Proxy *>
                Order allow,deny
                Allow from all
        </Proxy>
        ProxyPass / http://127.0.0.1:8000/
        ProxyPassReverse / http://127.0.0.1:8000/

        ErrorLog ${APACHE_LOG_DIR}/api.myweb.com.error.log
        CustomLog ${APACHE_LOG_DIR}/api.myweb.com.access.log combined

		RewriteEngine on
		RewriteCond %{SERVER_NAME} =www.api.myweb.com [OR]
		RewriteCond %{SERVER_NAME} =api.myweb.com
		RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
</VirtualHost>
```
**ServerName:** Es el nombre del sub dominio que apache reconocerá cuando se consulte.

**ProxyPass, ProxyPassReverse:** Son las directivas para poder reenviar el primer parámetro `/` a la dirección donde esta nuestra app. Por ejemplo: Cuando escriba `api.myweb.com` internamente apache me mandara a su puerto 8000, donde tendré acceso al API.

**ErrorLog, CustomLog:** Especifican la dirección de los archivos log.

**RewriteCond:** Estas reglas están hechas para poder redireccionar las consultas `http` a `https`, en caso no cuente con un certificado SSL, comente o elimine los 4 últimos comandos.


Note que para el ejemplo se esta usando `api.myweb.com.conf` como sub dominio, usted debe poner el nombre del su sub dominio.

### Paso 4: Enlazar y recargar el servicio de Apache2
Ahora tenemos que vincular el archivo `.conf` que se creo para que Apache lo pongo en su carpeta `/sites-enabled/` para esto se debe escribir lo siguiente:

```
$ sudo a2ensite api.myweb.com.conf
```
Con este comando Apache habilita el nuevo virtualHost, solo queda volver a cargar Apache2 para que contenga los nuevos cambios.
```
$ sudo service apache2 reload
```
Listo con esto apache se encuentra actualizado y la configuración de tu sub dominio ya esta en funcionamiento.

### Paso 5: Probar el sub dominio
Ahora solo queda probar el sub dominio para esto entren a su navegador y escribir su sub dominio, en nuestro ejemplo seria `http://api.myweb.com.conf`.

Listo ahora ya tiene un sub dominio dentro de su servidor usando Apache.

Para poder ver mas manuales parecidos a este puede ir a los [manuales](#) que DoApps nos ofrece.

### Autor

* **Joshua Navarro** - Desarrollador Backend - [GitHub](https://github.com/joshuanr5), [Twitter](https://twitter.com/JoshuaNavarroR1) 
