Hola, en esta oportunidad se dará la explicación breve, concisa y sencilla de como podemos desplegar un sitio web estático en AmazonS3.

### Pre-requisitos
* Contar con su directorio de sitio web estático que desea desplegar.
* Tener una cuenta de Amazon Web Service.

### Comencemos

1. Nos dirigimos a la siguiente URL de Amazon Web Service.
```
https://signin.aws.amazon.com/console
```
En este tutorial, contamos una URL personalizada.
```
https://doapps.signin.aws.amazon.com/console
```

Donde ingresamos nuestras credenciales de AWS e iniciamos sesión.

```
Credenciales
* Cuenta: doapps
* Nombre de usuario: doapps@doapps.me
* Contraseña: •••••••••••
```
<p align="center">
  <img  src="https://i.ibb.co/m0nzjPH/sesion.png">
</p>

3. Ahora nos encontramos dentro de la plataforma de AWS, seleccionamos en la parte superior izquierda lo siguiente:

```
Servicios > Almacenamiento > S3
```

![](https://i.ibb.co/hKwC5YW/s3.png)

4. Ahora procederemos a crear nuestro **Bucket**, el cual almacenará nuestro sitio web estático. Presionamos el botón **Crear bucket**.

![](https://i.ibb.co/BZ7Gpwr/BUCKET.png)

5. Procederemos a realizar la configuración de nuestro **Bucket**, completando con los siguientes datos.

```
1. Nombre y región
* Nombre del bucket: core.doapps.pe
* Región: EE.UU. ESTE(Ohio)
* Copiar configuración de un bucket existente:  plataforma-patrocinio.doapps.pe 
En esta oportunidad copiaremos una configuración existente.
Presionamos siguiente.

2. Configurar opciones
No realizamos ninguna modificación, presionamos siguiente.

3. Establecer permisos
No realizamos ninguna modificación, presionamos siguiente.

4. Revisión
No realizamos ninguna modificación, presionamos Crear bucket
```

![](https://i.ibb.co/P15td2L/config.png)

6. Felicidades, ya tenemos nuestro Bucket, ahora ingresamos y realizamos la configuración de los permisos correspondientes que debe tener nuestro Bucket para poder desplegar nuestro sitio web estático.

![](https://i.ibb.co/tcW8NXX/cbuccket.png)

7. Tendremos un Menú de la vista de nuestro Bucket y nos dirigimos a Propiedades.

![](https://i.ibb.co/DK8SRwp/prop.png)

8. Visualizaremos varias tarjetas, nos ubicamos dentro de **Alojamiento de sitios web estáticos**, y realizamos lo siguiente.
```
Visualizamos un Punto de enlace: http://core.doapps.pe.s3-website.us-east-2.amazonaws.com
El cual será nuestra URL para acceder a nuestro sitio web estático.
```

```
* Presionamos: Usar este bucket para alojar un sitio web
* Completamos el campo Documento de índice con nuestro archivo de inicio de nuestra página web (index.html). 
* Si contamos con un archivo para errores (error.html), rellenamos el campo Documento de error.
* Presionamos guardar.
```

![](https://i.ibb.co/9pvcFxs/fd.png)

9. Ya estamos casi listos para subir nuestros archivos y visualizar nuestra sitio web desplegado, pero antes haremos que sea público y cualquiera puede visualizarlo. En el Menú de la vista de nuestro Bucket, seleccionamos **Permisos** y luego **Política de Bucket**.

![](https://i.ibb.co/mb2NgyB/1.png)

10. Ingresamos el siguiente código, donde **yourbucketname**, tendrá el nombre de nuestro **Bucket**. Y presionamos en Guardar.

```
Ejemplo
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::yourbucketname/*"
    }
  ]
}
```

```
Nuestro Bucket
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::core.doapps.pe/*"
    }
  ]
}
```
![](https://i.ibb.co/c8W6zNB/3.png)

![](https://i.ibb.co/rdZcr1x/5.png)

11. Ahora nos dirigimos a Información General de nuestro Menú.

![](https://i.ibb.co/G3VNzPn/infogeneral.png)

12. Ahora haremos lo siguiente.
```
* Presionamos el botón Cargar.
```
![](https://i.ibb.co/hRvWMY5/6.png)

13. Nos mostrará la siguiente ventana, donde podremos añadir los archivos de nuestro sitio web estático. 
```
* Presionamos el botón Añadir Archivos.
```
![](https://i.ibb.co/0QYzrBN/7.png)

14. Ahora haremos lo siguiente.
```
* Seleccionamos los archivos de nuestro directorio de sitio web estático que desea desplegar.
* Presionamos Abrir
```
![](https://i.ibb.co/SVQmGJD/9.png)

15. Tendremos una visualización de todos los archivos que hemos seleccionado, ahora haremos lo siguiente.
```
1. Seleccionar archivos
* Presionamos siguiente.
2. Establecer permisos
* Presionamos siguiente.
3. Establecer propiedades 
* Presionamos siguiente.
4. Revisión
* Presionamos Cargar.
``` 
![](https://i.ibb.co/1qYpfdM/dsf.png)

16. Observamos que los archivos se están cargando, solo es cuestión de esperar y termine el proceso :).
![](https://i.ibb.co/wBpbnWN/12.png)

17. Felicidades nuevamente, ya termino de subir los archivos a nuestro Bucket.
![](https://i.ibb.co/bNMBKb3/13.png)

18. Ingresamos a la siguiente URL, para verificar que funcione correctamente.
```
 http://core.doapps.pe.s3-website.us-east-2.amazonaws.com
```
<p align="center">
  <img  src="https://i.ibb.co/VpVy0t0/aaa.png">
</p>

<p align="center">
<b> 🥇 Gracias por seguir este tutorial 👍 </b>

## Autor:
**Luis Yauri | Front-End Developer** :mortar_board:
