# Comprendiendo Request y Response

## Pregunta 1
**¿Cuáles son las dos diferencias principales que has visto anteriormente y lo que ves en un navegador web 'normal'? ¿Qué explica estas diferencias?**
- **Respuesta**:
  - En el navegador se ve el contenido ya procesado (HTML, CSS, JS), mientras que con curl ves el HTML en bruto.
  - El navegador carga recursos adicionales como imágenes, que curl no hace.
  - **Explicación**: curl es solo una herramienta de línea de comandos para hacer solicitudes HTTP, mientras que un navegador es un software completo para interpretar y mostrar páginas web.

## Pregunta 2
**Suponiendo que estás ejecutando curl desde otro shell ¿qué URL tendrás que pasarle a curl para intentar acceder a tu servidor falso y por qué?**
- **Respuesta**: La URL sería `http://localhost:8081`. Usas localhost porque el servidor falso (ncat) está ejecutando en tu propia máquina, y 8081 es el puerto.

## Pregunta 3
**La primera línea de la solicitud identifica qué URL desea recuperar el cliente. ¿Por qué no ves http://localhost:8081 en ninguna parte de esa línea?**
- **Respuesta**: En una solicitud HTTP típica, solo se utiliza el "path" y cualquier "query string" asociado.

## Pregunta 4
**Según los encabezados del servidor, ¿cuál es el código de respuesta HTTP del servidor que indica el estado de la solicitud del cliente y qué versión del protocolo HTTP utilizó el servidor para responder al cliente?**
- **Respuesta**: HTTP/1.1 200 OK. 200 OK es el código de estado HTTP, y HTTP/1.1 es la versión del protocolo HTTP.

## Pregunta 5
**Cualquier solicitud web determinada puede devolver una página HTML, una imagen u otros tipos de entidades. ¿Hay algo en los encabezados que crea que le dice al cliente cómo interpretar el resultado?**
- **Respuesta**: El encabezado Content-Type indica qué tipo de contenido está siendo enviado.

# ¿Qué sucede cuando falla un HTTP request?

## Pregunta 1
**¿Cuál sería el código de respuesta del servidor si intentaras buscar una URL inexistente en el sitio generador de palabras aleatorias?**
- **Respuesta**: 404, que significa "No encontrado".

## Pregunta 2
**¿Qué otros códigos de error HTTP existen?**
- **Respuesta**: 
  - 200: OK
  - 301: Moved Permanently
  - 302: Found
  - 400: Bad Request
  - 404: Not Found
  - 500: Internal Server Error

## Pregunta 3
**¿Cuál es la principal diferencia entre 4xx y 5xx?**
- **Respuesta**: Los códigos 4xx son errores causados por el cliente y los códigos 5xx indican problemas en el servidor.

# ¿Qué es un cuerpo de Request?

## Pregunta 1
**Cuando se envía un formulario HTML, ¿con qué URL deberías reemplazar Url-servidor-falso en el archivo anterior?**
- **Respuesta**: Se remplaza con `http://localhost:8081`.

## Pregunta 2
**¿Cómo se presenta al servidor la información que ingresó en el formulario? ¿Qué tareas necesitaría realizar un framework SaaS como Sinatra o Rails para presentar esta información en un formato conveniente a una aplicación SaaS escrita, por ejemplo, en Ruby?**
- **Respuesta**: La información se presenta en formato application/x-www-form-urlencoded. Frameworks como Sinatra o Rails la procesan y convierten en un objeto o diccionario.

# Preguntas Adicionales

- **¿Cuál es el efecto de agregar parámetros URI adicionales como parte de la ruta POST?**
  - No afectan el cuerpo del mensaje POST.
- **¿Cuál es el efecto de cambiar las propiedades de nombre de los campos del formulario?**
  - Cambiará cómo los datos son etiquetados en el cuerpo del mensaje POST.
- **¿Puedes tener más de un botón Submit?**
  - Sí, se puede. El servidor identificará cuál se clickeó mediante el valor y nombre del botón en el cuerpo del POST.
- **¿Se puede enviar el formulario mediante GET en lugar de POST?**
  - Sí, pero los datos del formulario se añadirán a la URL.
- **¿Qué otros verbos HTTP son posibles en la ruta de envío del formulario?**
  - PUT, PATCH, DELETE son posibles pero requieren JavaScript para forzar su uso en un formulario HTML.

# HTTP sin estados y cookies

## Pregunta 1
**Prueba las dos primeras operaciones GET anteriores. ¿Cuáles son las diferencias en los encabezados de respuesta que indican que la segunda operación está configurando una cookie?**
- **Respuesta**: En la respuesta HTTP de la segunda operación, deberías ver un encabezado llamado `Set-Cookie`. Este encabezado especifica la cookie que se debe almacenar en el cliente. Contiene el nombre de la cookie, el valor, y otros atributos como el dominio, el tiempo de expiración, entre otros. Esto indica que el servidor está intentando establecer una cookie en tu navegador o cliente.

## Pregunta 2
**Bien, ahora supuestamente "logged in" porque el servidor configuró una cookie que indica esto. Sin embargo, si intentaa GET / nuevamente, seguirá diciendo "Logged: false". ¿Qué está sucediendo?**
- **Respuesta**: Cuando usas `curl`, a menos que le digas específicamente que guarde y utilice cookies, no mantendrá el estado de la sesión entre múltiples solicitudes. En un navegador, la cookie se guardaría y se enviaría automáticamente con cada solicitud posterior al mismo servidor. En `curl`, necesitas especificar un archivo donde guardar las cookies con `--cookie-jar` y luego usar `--cookie` para enviar esas cookies en solicitudes posteriores..

## Pregunta 3
**Al observar el encabezado Set-Cookie o el contenido del archivo cookies.txt, parece que podría haber creado fácilmente esta cookie y simplemente obligar al servidor a creer que ha iniciado sesión. En la práctica, ¿cómo evitan los servidores esta inseguridad?**
- **Respuesta**: Los servidores toman varias medidas para asegurarse de que las cookies no puedan ser falsificadas o robadas:
- **HTTPS**: Asegura que las cookies se transmitan de forma segura.
- **Atributos de Cookie**: Como `HttpOnly` y `Secure` para mejorar la seguridad.
- **Tokens CSRF**: Para prevenir ataques de falsificación de solicitudes entre sitios.
- **Rotación de Sesiones**: Cambiar los identificadores de sesión con regularidad.
- **Autenticación de Dos Factores**: Agrega una capa extra de seguridad.
- **Políticas de Cors**: Controlan qué dominios pueden acceder a las cookies.
Espero que este formato te sea de utilidad.
