En el siguiente documento detallamos el estándar que usamos para diseñar nuestras APIs RESTful, para ello detallaremos las reglas y convenciones usadas en el desarrollo de nuestras APIs.

Si desean sugerir mejoras o solicitar ejemplos extras puedes dejar un issue indicándolo.

## Estructura de las rutas

Las rutas deben ser entendidas por cualquier desarrollador, para esto se requiere de mantener un patrón constante a la hora de crearlos. Este patrón es llamado ***enfocado a entidades*** o ***patrones de colección*** (como lo hace [Microsoft en su guía](https://github.com/Microsoft/api-guidelines/blob/vNext/Guidelines.md#93-collection-url-patterns)).

```
GET https://api.myproject.com/v1.0/empresas/10/empleados
```

En el ejemplo anterior se puede ver como obtener a los empleados de la empresa con identificador 10. El patrón es el siguiente:

```
GET https://{serviceRoot}/{collection}/{id}/{collection}/{id}/...
```

Las rutas aceptaran los métodos HTTP que se verán en la siguiente sección.

## Métodos HTTP

| **HTTP Method** | **Description** |
| --- | --- |
| GET | Para obtener un recurso o listar un arreglo de recursos. |
| POST | Para crear un recurso o ejecutar una operación compleja. |
| PUT | Para actualizar un recurso. |
| DELETE | Para eliminar un recurso. |
| PATCH | Para actualizar un recurso de forma parcial. |

### Método GET

El método GET es usado para obtener información de toda una entidad o de una en específico.

Como ejemplo podemos imaginar que queremos obtener todos los proyectos que están asignados a un empleado.

```
GET https://api.myproject.com/v1.0/empleados/37/proyectos
```

Una respuesta seria un Array con los proyectos asignados al empleado 37.

### Método POST

Este método se utiliza en su mayoría para crear nuevos recursos para las entidades que maneja el servidor, también es usado para el manejo de funciones complejas. Una de sus otras características es que este método es idempotente.

Como ejemplo podemos imaginar que deseamos registrar a un nuevo empleado al sistema.

```
POST https://api.myproject.com/empleados (información en el body)
```

Note que no se especifica, ni se debería especificar el id del nuevo empleado debido a que los servidores tienden a generar el mejor identificador para el nuevo recurso.

El resultado de esta consulta nos devolverá en su mayoría una respuesta vacía con la cabecera **`location`** la cual tendrá la ruta para obtener el detalle de, en el caso del ejemplo, nuestro nuevo empleado.

```
201 Created
Location: http://api.myproject.com/empleados/37
```

### Método DELETE

Este método se utiliza para eliminar un recurso específico de una entidad.

Como ejemplo eliminaremos un producto de nuestra carta debido a que se descontinuó en el mercado.

```
DELETE https://api.myproject.com/productos/65
```

No te que es necesario especificar el identificador del producto, en caso que no se especifique el servidor no realizará ninguna acción y mandará el mensaje de error correspondiente.

El resultado de una consulta en su mayoría tiende a ser vacío con el estado `202 Accepted`, pero en algunos casos es necesario mandar un mensaje informativo para que sea usado por el cliente que consume el servicio junto con el código de estado `200 OK`.

### Método PUT

Este método se utiliza para modificar información de un recurso en específico, tiende a ser idempotente lo cual significa que el uso de este servicio no cambiará el resultado a menos que se modifique los parámetros.

Como ejemplo imaginemos que queremos modificar la fecha de entrega de un proyecto.

```
PUT https://api.myproject.com/proyectos/54 (información en el body)
```

El resultado de esta consulta es un objeto con la información actualizada del recurso (proyecto con identificador 54).

### Método PATCH

## HTTP Status Code

Los códigos de estado en una respuesta del servidor son importantes, debido a que ayuda al cliente a entender que ha sucedido con su consulta: si fue exitosa, si lo hizo mal o si ocurre algún problema en el servidor.

| **Rango** | **Descripción** |
| --- | --- |
| 2xx | Ejecución exitosa. |
| 4xx | Hubo problemas con la petición. |
| 5xx | Error del servidor. |

Cada rango tiene sus diferentes códigos de estado, los cuales se usan para situaciones más específicas, como se muestra en la siguiente tabla:

| **Status Code** | **Descripción** |
| --- | --- |
| 200 OK | Ejecución de la consulta de manera exitosa |
| 201 Created | Se usa para responder a los métodos POST que crean recursos en las entidades. Si el recurso ya estaba creado, entonces el server debería retornar el código 200 OK. |
| 400 Bad Request | La consulta puede no ser entendida por el servidor. Se usa este código para lo siguiente: <ul> <li>La información como parte del body no puede ser convertida al tipo de información necesaria.</li> <li>La información no es del formato que se requiere.</li> <li>Los campos requeridos no están disponibles.</li> <li>Errores de validaciones de tipo de datos.</li> </ul> |
| 401 Unauthorized | La consulta requiere de autenticación y esta no ha sido proporcionado o es invalido.Note la diferencia entre este y el 403 Forbidden |
| 403 Forbidden | El cliente no tiene autorización para acceder al recurso, así sus credenciales sean válidas. |
| 404 Not Found | El servidor no ha encontrado un match con la URI. Esto puede significa que la URI es incorrecta o los recursos no están disponibles. Por ejemplo, puede que no exista información de un recurso en la base de datos con la llave dada. |
| 405 Method Not Allowed | El servidor no ha implementado el método HTTP consultado. |
| 500 Internal Server Error | Es es un error del sistema o la aplicación, y generalmente indica que aunque el cliente haya proporcionado una consulta correcta, algo inesperado a salido mal en el servidor. |
| 503 Service Unavailable | Es servidor no puede realizar la consulta debido a que se encuentra en mantenimiento temporalmente. |

## Status Code permitidos por cada método HTTP

| **Status Code** | **200 Success** | **201 Created** | **400 Bad Request** | **404 Not Found** | **500 Internal Server Error** |
| --- | --- | --- | --- | --- | --- |
| GET | X |   | X | X | X |
| POST | X | X | X | X | X |
| PUT | X |   | X | X | X |
| PATCH | X |   | X | X | X |
| DELETE | X |   | X | X | X |

## Queries

En un API REST las rutas o endpoints suelen estar acompañadas de ***queries*** como parte de ella para lograr realizar consultas, en su mayoría de tipo `GET`, más específicas o complejas.

Como ejemplo podríamos necesitar las asistencias de nuestros empleados en el mes de mayo y que me retornen de manera ordenada por la fecha de creación, la cual se ve algo así:

```
GET https://api.myproject.com/asistencias?month=mayo&amp;sort=createdAt,desc
```

Como se puede ver los ***queries*** se usan después del signo **`?`** y se puede usar varios a la vez separados por **` `** (espacio). En este caso hemos hemos usado **`month`** y **`sort`** para poder lograr con el cometido.

Iremos a explicar algunos queries generales a la hora de realizar un API RESTful, estos son **Filtros**, **Ordenamiento** y **Paginación.**

### Filtros

Los filtros tiene como objetivo darle condiciones, en su mayoría de igualdad, a las consultas hechas por el clientes para obtener información específica de una entidad. Este tipo de filtro pueda puede usar varios operadores los cuales se vean en la siguiente tabla.

| **Operador** | **Descripción** | **Ejemplo** |
| --- | --- | --- |
| Comparison Operators |
| eq | Igualdad | city eq &#39;Redmond&#39; |
| ne | No igualdad | city ne &#39;London&#39; |
| gt | Mayo que | price gt 20 |
| ge | Mayor o igual que | price ge 10 |
| lt | Menor que | price lt 20 |
| le | Menor o igual que | price le 100 |
| Logical Operators |
| and | Logical and | price le 200 and price gt 3.5 |
| or | Logical or | price le 3.5 or price gt 200 |

El query que se debe usar es **`filter`** , el cual se usa con corchetes **`[ ]`** y se debe usar por cada criterio que se desea.

Por ejemplo queremos listar los empleados que se encuentren en una ciudad especifica, la llamaremos **A**, y que sean menores de 35 años pero mayores de 20.

```
GET https://api.myproject.com/empleados?filter[city eq]=A&amp;filter[agelt]=35&amp;filter[age gt]=20
```

Esta consulta te traería los empleados que se desean en el ejemplo, note cómo usamos el query **`filter`** por cada criterio.

Otro ejemplo un poco más complejo sería si deseamos obtener los empleados que no son de género masculino, que viven en la ciudad de **A** o en la ciudad **B**.

```
GET[https://api.myproject.com/empleados?filter[city](https://api.myproject.com/empleados?filter%5Bcity) eq]=A&amp;filter[or city eq]=B&amp;filter[or genre ne]=Masculino
```

Como se ve este diseño es muy flexible, permitiendo mejorar el resultado de la consulta de grandes formas.

### Ordenamiento

Para obtener información ordenada al momento de listar una entidad se usa el query de ordenamiento llamado **`sort`** , a este query se le especifica el atributo que se desea ordenar y si es ascendente o descendente, separados por un espacio ` `. Si se desea agregar más atributos en el criterio de ordenamiento este se hará seguido de una coma **`,`** y siguiendo las mismas reglas previstas.

Como ejemplo práctico podemos imaginar que deseamos obtener las lista de nuestros empleados ordenados por el número de proyectos que han realizado y de segunda prioridad ordenarlo por nombres.

```
GET https://api.myproject.com/empleados?sort=projectsCompleted desc,names
```

Este es un ejemplo que quizá se escapa del documento o de esta sesión pero que siento que se debería hacer notar. Supongamos que la tabla ***Empleados*** no guarda el número de proyectos que ha completado cada empleado, sino que ello es un valor que se obtiene de la relación que tiene la tabla ***Empleados*** y la tabla ***Proyectos*** (por medio de un `count`), esto quiere decir que las las entidades de las rutas o endpoints no son entidades directas de la base de datos como se podría apreciar en primera instancia, sino que por dentro la lógica puede llegar a ser mucho mayor combinando varias tablas y dando un resultado de manera general. En el caso del ejemplo, el número de proyectos que terminó un empleado hace referencia a información de empleados por eso la ruta **`/empleados`** lo define perfectamente.

### Paginación

Cuando creas un API en su mayoría se tiende a diseñar para que un aplicativo móvil o web lo consuman, debido a esto el API debe tener funcionalidades que en una aplicación móvil se ve con frecuencia y una de estas es la ***paginación*** que permite al cliente hacer una partición de páginas al total de datos de una entidad y entregar el subconjunto de datos que se le especifica. Esta característica se ve muy a menudo en las tablas, y es debido a que la cantidad de información que se podría obtener de un API puede ser tan grande que es necesario consumirla por partes.

Esta funcionalidad tiene dos queries para que funcione de manera adecuada una es **`page`** la cual indica la página **n** a obtener de la partición que se realizará y **`per_page`** que indica la cantidad de datos que habrá por página.

Para entender esto imaginemos que se desea listar los mensajes que el trabajador **A** con identificador **9** ha enviado, pero solo deseamos obtener los 10 mensajes primeros mensajes (por ejemplificación se obtendrá los mensajes independientemente del destinatario).

```
GET https://api.myproject.com/empleados/9/mensajes?page=1&amp;per\_page=10
```

Ahora supongamos que deseamos obtener los 10 mensajes siguientes entonces solo se debe modificar el query **`page`** de 1 a 2.

```
GET https://api.myproject.com/empleados/9/mensajes?page=2&amp;per\_page=10
```

Debido que en algunos casos se es necesario saber la cantidad de elementos que hay en la entidad consultada, la cantidad de páginas de la partición que se hizo y la página actual, se debe mandar esta información por medio de la cabecera de la respuesta (**header response**) con los siguientes atributos:

- **Total-Count:** Es la cantidad de elementos que tiene la entidad.
- **Total-Pages:** Es la cantidad de páginas que tiene la partición que se le hizo al total de datos.
- **Current-Page:** Es la página actual que se solicitó en la consulta.

### Otros

También en muchos casos se suele encontrar con varios otras funciones que debería aceptar las URI de nuestra API, estos pueden llegar a variar dependiendo del caso de negocio que se presente en el momento. Unos claros ejemplos puede ser

- **Búsqueda:** Que se realiza para hacer búsqueda simples o complejas (que conllevan varios atributos). Se debe usar el query **`search`** seguido de el valor que se desea buscar.
- **Obtener los más cercanos:** Esta funcionalidad normalmente tiene como fin hacer un filtro o un ordenamiento basado en la distancia que se encuentra las entidades (tómese como ejemplo los ***restaurantes***). Quizá esta es una de las más complicadas pero a su vez suelen ser pedidas cuando se trabaja con mapas en la cual normalmente se utiliza dos queries que son **`location`** para especificar el punto (la ***latitud*** y ***longitud***) de referencia para obtener la distancia y **`ratio`** para especificar que tan grande debe ser la distancia en ***Km***.

Estos solo son dos ejemplos de los muchos que pueden haber que dependerá mucho del caso de negocio.

## Errores

Para nuestro diseño de las APIS RESTful se desean mandar los mensajes que serán usados para que el cliente final pueda verlo, y también se manda un campo de detalle que explique cuál es el error específico, para que el cliente, que usa el API, pueda saber qué es lo que está sucediendo. Este manejo de errores se puede ver en los códigos **`4xx`** y **`5xx`.**

```json
{
    "message": "Ocurrió un error en el servidor",
    "details": "'Email' field must be and email"
}
```

## Recomendaciones

En esta sesión se verán algunas recomendaciones al diseñar nuestra API RESTful que no se han mencionado en sesiones previas.

### Autenticación con bearer Token

Debido a que las APIS son stateless que quiere decir que toda la información que necesita el servidor debe estar contenido en la consulta, la cual una forma de poder hacer que el servidor sepa quien eres y si tienes acceso al sistema. Esto se realiza medio de un token que es un enfoque stateless para poder enviar información de del usuario y el servidor logre identificarlo.

Para esto usamos una librería muy conocida que se llame [JWT](https://jwt.io/) la cual cuenta con muchas funcionalidades una de estas es la de expiración que es muy importante para la seguridad de tu API.

Este token se envía por medio del header, haciendo uso de su atributo **`Authorization`** y el token debe tener el prefijo `Bearer ` note el espacio.

Como ejemplo del header se podría realizar de esta forma

```json
{
    "Authorization": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6bnVsbH0.HoQRbTNid60fthXJECUzzoBjTw7avSWuaRx8hGqs0VQ"
}
```

### Fuentes

[https://github.com/cloudfoundry/cc-api-v3-style-guide](https://github.com/cloudfoundry/cc-api-v3-style-guide#filtering)

[https://github.com/Microsoft/api-guidelines/blob/vNext/Guidelines.md](https://github.com/Microsoft/api-guidelines/blob/vNext/Guidelines.md)