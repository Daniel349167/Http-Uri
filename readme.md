Comprendiendo Request y Response
Pregunta 1
¿Cuáles son las dos diferencias principales que has visto anteriormente y lo que ves en un navegador web 'normal'? ¿Qué explica estas diferencias?

a. En el navegador se ve el contenido ya procesado (HTML, CSS, JS), mientras que con curl ves el HTML en bruto.
b. El navegador carga recursos adicionales como imágenes, que curl no hace.
c. Por qué las diferencias: curl es solo una herramienta de línea de comandos para hacer solicitudes HTTP, mientras que un navegador es un software completo para interpretar y mostrar páginas web.
Pregunta 2
Suponiendo que estás ejecutando curl desde otro shell ¿qué URL tendrás que pasarle a curl para intentar acceder a tu servidor falso y por qué?

La URL que tendrías que pasarle a curl sería http://localhost:8081. Usas localhost porque el servidor falso (ncat) está ejecutando en tu propia máquina, y 8081 es el puerto en el que estás escuchando.
Pregunta 3
La primera línea de la solicitud identifica qué URL desea recuperar el cliente. ¿Por qué no ves http://localhost:8081 en ninguna parte de esa línea?

En una solicitud HTTP típica, la URL completa no se incluye en la primera línea. En su lugar, se utiliza solo el "path" y cualquier "query string" asociado. En este caso, el "path" es /, que representa la raíz del recurso solicitado en el servidor.
Pregunta 4
Según los encabezados del servidor, ¿cuál es el código de respuesta HTTP del servidor que indica el estado de la solicitud del cliente y qué versión del protocolo HTTP utilizó el servidor para responder al cliente?

En la respuesta, la línea HTTP/1.1 200 OK. 200 OK es el código de estado HTTP, y HTTP/1.1 es la versión del protocolo HTTP utilizada por el servidor.
Pregunta 5
Cualquier solicitud web determinada puede devolver una página HTML, una imagen u otros tipos de entidades. ¿Hay algo en los encabezados que crea que le dice al cliente cómo interpretar el resultado?.

El encabezado Content-Type generalmente indica qué tipo de contenido está siendo enviado. Podría ser text/html para una página HTML, image/jpeg para una imagen JPEG, etc. Esto ayuda al cliente a saber cómo interpretar los datos recibidos.
Qué sucede cuando falla un HTTP request
Pregunta 1
¿Cuál sería el código de respuesta del servidor si intentaras buscar una URL inexistente en el sitio generador de palabras aleatorias? Prueba esto utilizando el procedimiento anterior.

Si intentas buscar una URL inexistente, el código de respuesta HTTP más probable sería 404, que significa "No encontrado".
Pregunta 2
¿Qué otros códigos de error HTTP existen?

200: OK, la solicitud ha tenido éxito.
301: Moved Permanently, el recurso se ha movido permanentemente a otra URL.
302: Found, el recurso se encuentra temporalmente en otra URL.
400: Bad Request, la solicitud es incorrecta.
404: Not Found, el recurso solicitado no se encuentra.
500: Internal Server Error, error interno del servidor.
Pregunta 3
¿Cuál es la principal diferencia entre 4xx y 5xx?.

Los códigos 4xx indican errores causados por el cliente. Es decir, el cliente parece haber errado la solicitud.
Los códigos 5xx indican problemas en el servidor. Aquí el servidor falló al cumplir una solicitud válida.
Qué es un cuerpo de Request
Pregunta 1
Cuando se envía un formulario HTML, se genera una solicitud HTTP POST desde el navegador. Para llegar a tu servidor falso, ¿con qué URL deberías reemplazar Url-servidor-falso en el archivo anterior?

Se remplaza con http://localhost:8081 para acceder a tu servidor falso.
Pregunta 2
¿Cómo se presenta al servidor la información que ingresó en el formulario? ¿Qué tareas necesitaría realizar un framework SaaS como Sinatra o Rails para presentar esta información en un formato conveniente a una aplicación SaaS escrita, por ejemplo, en Ruby?

La información del formulario se presenta en el cuerpo del