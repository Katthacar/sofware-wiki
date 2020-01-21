## Crear un droplet en DigitalOcean
### Pre-requisitos
- Tener una cuenta en DigitalOcean. Si no cuenta con una cuenta registrarse en [Registrarse - DigitalOcean](https://cloud.digitalocean.com/registrations/new)

### Conceptos básicos
#### DigitalOcean
DigitalOcean (DO) es un [IaaS](https://en.wikipedia.org/wiki/Infrastructure_as_a_service) que te ofrece servicios de infraestructura alojados en la nube, facilitando el mantenimiento y escalabilidad de tu servidores (CPU, RAM, etc.).

#### Droplet
DO brinda diferentes servicios tales como Spaces, Volumes y entre otros. En el presente capitulo hablaremos de unos de sus productos mas usados que son los Droplets, en pocas palabras son maquinas virtuales basadas en [Linux](https://es.wikipedia.org/wiki/GNU/Linux) que te ofrecen la arquitectura necesaria para crear tu servidor. Si desea profundizar mas siempre puede consultar a la [documentación de su producto](https://www.digitalocean.com/docs/droplets/).

### Creación del droplet
Una vez ya ingresado en DO le aparecerá el [dashboard](https://cloud.digitalocean.com) donde podrá ver y crear los distintos servicios. 
- En el dashboard dar click en **create** y elegir **Droplets**.
- Se dirigirá a una pantalla para seleccionar las características de tu droplet.
- En la sección **Choose an image** selecciona **Ubuntu 18.04 x64**.
- En la sección **Choose a size** que en otras palabras es el precio de su droplet elegir la mas baja ya que es lo necesario para este tutorial (Si desea crear un droplet para producción, es necesario que decida bien esta opción).
- En la sección **Choose a datacenter region** elegir la region mas cercana.
- En la sección **Finalize and create** escribir el nombre de su droplet.
- Para finalizar darle click en **create**.

### ¿Qué puedo hacer a partir de aquí?
Al final de este manual, usted ya cuenta con un droplet con Ubuntu 18.04 x64 en la cual podra configurar e instalar lo que usted desee. Les dejao el siguiente manual [Configuració incial para Ubuntu 18.04 x64](https://github.com/doapps/software/wiki/Configuración-inicial-de-Ubuntu-18.04-x64) para seguir aprendiendo o siempre puede visitar la [página del contenido](https://github.com/doapps/software/wiki/Manuales-inicio) para mas manuales.