Ahora todo proyecto; sea para mobil, web o desktop; hace uso de información la cual almacena en bases de datos. Estas bases de datos que pueden ser SQL o noSQL, ayuda al desarrollador a poder guardar y obtener información acerca del sistema que se use.

La información es uno de los elementos mas valiosos de una organización, por ello mismo una de las amenazas que tiene toda organización es el robo de su información o secuestro por medio de [Ransomware](https://es.wikipedia.org/wiki/Ransomware). Una solución básica y muy eficiente es el realizar backups, y es lo cual aprenderemos en este manual.

### Pre-requisitos
- Tener una cuenta de **Amazon Web Services** y contar con su respectivas **AWS Access Key** y **AWS Secret Access Key** . En caso que no lo tengas puedes visitar [esta página](https://supsystic.com/documentation/id-secret-access-key-amazon-s3/).
- Tener un servidor ubuntu, donde se encuentre alojado tu base de datos: MySQL o MongoDB (otros serán visto luego).

### Instalar AWS CLI
Usaremos AWS CLI para poder tener acceso al S3 storage de Amazon Web Services, para instarlo daremos uso del `apt`.

```console
sudo apt update
sudo apt install awscli
```
Le das `Yes` y terminara la instalación.

### Crear un script para automatizar el proceso
Crearemos un script el cual realizara el siguiente proceso:

- Realizar el backup de la base de datos
- Comprimir el backup en .7z
- Subir el archivo comprimido a tu *bucket* de S3
- Eliminar el backup comprimido

Empezaremos creando el archivo `script.sh` en la dirección `/home/<username>/BACKUPS`

```console
sudo nano /home/<username>/BACKUPS/script.sh
```

Empezaremos a escribir el Script, lo explicaremos parte por parte.

#### Declarar variables
Declararemos las variables que se usaran a lo largo del script.
```console
#!/bin/sh

# Variables
BACKUP_ROOT_FOLDER=/home/<username>/BACKUPS
DB_NAME=<dbname>
DB_PORT=<dbport>
DB_USER=<dbuser>
DB_PASS=<dbpass>
AWS_S3_BUCKET_NAME=<your_bucket_name>
AWS_S3_FOLDER_NAME=<your_folder_name>
```
Explicación:
`BACKUP_ROOT_FOLDER`: Es el folder donde se guardara el script.sh, los backups y los logs.
`DB_NAME`: Es el nombre de la base de datos la cual se hara el backup.
`DB_PORT`: Es el puerto de la base de datos en MySQL por defecto es 3306.
`DB_USER`: Es el usuario que tiene acceso a la base de datos.
`DB_PASS`: Es la contraseña del usuario
`AWS_S3_BUCKET_NAME`: Es el nombre del bucket que se creo en Amazon Web Services S3.
`AWS_S3_FOLDER_NAME`: Es el folder dentro del bucket para tener los archivos mas organizados.

#### Creamos la carpeta donde se guardará los backups
```console
...

# Creamos la carpeta del backup
DIR=$AWS_S3_FOLDER_NAME-$(date +%F)
DEST=$BACKUP_ROOT_FOLDER/$DIR
mkdir -p $DEST
```

#### Hacemos el backup para MySQL y MongoDB
Para MySQL
```console
...

# generar backup
mysqldump -u$DB_USER -p$DB_PASS $DB_NAME >  $DEST/$DIR.sql
```

#### Comprimir  y eliminar la carpeta
Instalar 7z con el siguiente comando
```console
sudo apt install p7zip-full
```

Comprimir
```console
...

# Comprimir carpeta de backup en un archivo 7z
BACKUP_FILE=$DIR.7z
7z a $BACKUP_ROOT_FOLDER/$BACKUP_FILE $DEST
```

Eliminar carpeta
```console
...

# eliminar carpeta de backup
rm -rf $DEST
```

#### Enviar el backup a S3

```console
...

# subir backup comprimido a s3
/usr/bin/aws s3 cp --storage-class STANDARD_IA --sse AES256 $BACKUP_ROOT_FOLDER/$BACKUP_FILE s3://$AWS_S3_BUCKET_NAME/$AWS_S3_FOLDER_NAME/
```

#### Eliminar el backup comprimido y crear un log

``` console
...

# eliminar archivo 7z
rm $BACKUP_ROOT_FOLDER/$BACKUP_FILE

# grabar un registro en log para tener tracking
echo "$DIR $(date)" >> $BACKUP_ROOT_FOLDER/backup.log
```

#### Ultimos pasos
Ahora debemos dar permisos al script para que sea ejecutable
```console
sudo chmod 755 /home/<username>/BACKUPS/script.sh
```

Listo esto seria lo necesario para tener el script para realizar el backup y subirlo a amazon Web Services S3. Para probarlo ejecuta el siguiente comando

```console
/home/<username>/BACKUPS/script.sh
```

#### Crear una programación de tareas que se repita cada día
Crearemos una programación de tareas usando **crontab**, para ellos debemos especificar 5 puntos: minutos, horas, día, mes, día de la semana.

```console
crontab -e 45 1 * * * /home/ubuntu/BACKUPS/script.sh
```

Con este comando se realizara el script todos los días, a la 1:45h.

#### Palabras finales
Con esto ya tienes los backups de tu base de datos automatizada y subidas a S3.

### Autor: 
### [Joshua Navarro](https://github.com/joshuanr5) | **Backend Developer** :octocat: 