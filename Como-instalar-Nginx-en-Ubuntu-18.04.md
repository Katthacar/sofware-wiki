## Instalar Nginx
Prerequisito: 
```# ufw enable``` 
```# ufw allow OpenSSH```

https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-18-04

## Instalar certificado SSL
Nota: `sudo certbot --nginx -d api.doapps.pe``
https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-16-04


## Instalar la ultima versión de node y npm

Se recomienda Install Node.js from the NodeSource repository: https://github.com/nodesource/distributions

```
# Using Ubuntu
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install -y nodejs
```

https://linuxize.com/post/how-to-install-node-js-on-ubuntu-18.04/

node source:
https://github.com/nodesource/distributions/blob/master/README.md

Posible problema con certificados inválidos:
https://tecadmin.net/expired-key-expkeysig-with-apt/?cerror=missing-input-response#respond

## Instalar yarn
https://yarnpkg.com/lang/en/docs/install/#debian-stable

## Instalar PM2

`npm install pm2@latest -g`

## Desinstalar paquetes de forma permanente en ubuntu
https://vitux.com/how-to-uninstall-programs-from-your-ubuntu-system/

## Instalar mysql 8 
https://www.tecmint.com/install-mysql-8-in-ubuntu/

Configuración de usuarios remotos:

**Crear un usuario remoto con privilegios de administrador**

`CREATE USER 'administrator'@'165.22.130.179' IDENTIFIED BY 'AdminPass1#';`

`GRANT ALL PRIVILEGES ON *.* TO 'administrator'@'165.22.130.179';`

**Listar usuarios actuales**
`SELECT user,host FROM mysql.user;`

**Eliminar usuario**
`DROP User 'root'@'165.22.130.179';`

Posible error mysql8

Error: ER_NOT_SUPPORTED_AUTH_MODE: Client does not support authentication protocol requested by server; consider upgrading MySQL client
Solución:
`ALTER USER 'yourusername'@'localhost' IDENTIFIED WITH mysql_native_password BY 'youpassword';
FLUSH PRIVILEGES;`

conexión remota
`mysql -h doapps-mysql-prod.c1okpv6cpklp.us-east-2.rds.amazonaws.com -uroot -p`
## Instalar MongoDB
Usar la guía oficial: https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/
*Importante: en el último paso no usar:
```sudo apt-get install -y mongodb-org```

En lugar de eso usar:
```sudo apt-get install -y mongodb```

Usar esta guia para configurar el usuario admin
https://www.tecmint.com/install-mongodb-on-ubuntu-18-04/

Configurar usuario
```db.createUser({user:"root", pwd:"root", roles:[{role:"root", db:"admin"}]})``` 

Robo3T 1.2 como cliente mongo'
Si tienes problemas en Robot3T para conectarte via SSH revisar esto: https://eldevsin.site/problema-conexion-ssh-en-robo3t-macos/

Conexion remota:
Revisar esta configuración: https://www.mkyong.com/mongodb/mongodb-allow-remote-access/
Usar la IP pública del mismo servidor de BD

`mongo -u root -p root 142.93.172.57:27017 --authenticationDatabase admin`

Conexión local a una bd específica:

`mongo -u root -p root localhost:27017/blp --authenticationDatabase admin`

## Configuración UFW

https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-18-04
https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands

```
sudo ufw default deny incoming
sudo ufw default allow outgoing

sudo ufw allow from 165.22.130.179/32 to any port 27017
sudo ufw allow from 165.22.130.179/32 to any port 3306

Forma clásica

`sudo ufw allow 4000`

`sudo ufw delete allow 4000`

`sudo ufw delete 3`
```

## Configuracion timezone ubuntu

configurar timezone `sudo dpkg-reconfigure tzdata`

Ver la configuración actual`timedatectl`

## Reverse Proxy NGINX

https://www.linode.com/docs/web-servers/nginx/use-nginx-reverse-proxy/

`/etc/nginx/conf.d/main.conf`

test: `sudo nginx -t`

reload: `sudo nginx -s reload`

## Modificar el tamaño máximo permitido de un archivo a subirse al servidor 
Error - Request Entity Too Large
Solución: 
- archivo `/etc/nginx/nginx.conf`
    client_max_body_size 500M
    
- sudo service nginx restart

## Liberar puertos


Listar todos procesos que escuchan puertos
$ sudo lsof -i -P -n | grep LISTEN 

Listar todos procesos que ejecutan un proceso nodejs
$ sudo lsof -i -P -n | grep node

Listar PID por puerto especifico del proceso
$ lsof -i tcp:3000

Listar PID por nombre del proceso
$ ps ax | grep firefox

Liberar puerto matando proceso
$ kill -9 PID

Listar PID por puerto:
$ lsof -i :8080
## Usar crontab

Listar PID and program name
$ netstat -tulpn

https://geekytheory.com/programar-tareas-en-linux-usando-crontab

## Uso de puertos para aplicaciones

del 4000 al 4999

## Instalar Apache Tomcat

https://tecadmin.net/install-tomcat-9-on-ubuntu/

No olvidar dar los permisos al usuario `ubuntu` para acceder a las carpetas respectivas:

Step 4: Update Permissions
The tomcat user that we set up needs to have access to the Tomcat installation. We'll set that up now.

Change to the directory where we unpacked the Tomcat installation:

`cd /opt/tomcat`

Give the tomcat group ownership over the entire installation directory:

`sudo chgrp -R tomcat /opt/tomcat`

Next, give the tomcat group read access to the conf directory and all of its contents, and execute access to the directory itself:

`sudo chmod -R g+r conf`

`sudo chmod g+x conf`

Make the tomcat user the owner of the webapps, work, temp, and logs directories:

`sudo chown -R tomcat webapps/ work/ temp/ logs/`

Now that the proper permissions are set up, we can create a systemd service file to manage the Tomcat process.

Más info: https://tecadmin.net/install-tomcat-9-on-ubuntu/