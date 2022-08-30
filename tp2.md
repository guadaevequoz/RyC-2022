## Práctica 2 - Capa de Aplicación - HTTP

## Introducción

### 2. ¿Cuál es la función de la capa de aplicación?

La capa de aplicación es la que se encarga de cómo representar e interpretar los datos. Hace una conversion y codificación de datos de la compu a datos de lenguaje natural. Define la semántica de los mensajes y tambien el formato. Define cómo va a ser el dialogo con el usuario.

### 3. Si dos procesos deben comunicarse:

### a. ¿Cómo podrían hacerlo si están en diferentes máquinas?

Dos procesos que residen en distintas terminales se comunican intercambiando mensajes por medio de una red. Un proceso emisor crea y envia mensajes a la red, mientras que el receptor recibe los mensajes y responde con otros mensajes.

### b. Y si están en la misma máquina, ¿qué alternativas existen?

Si dos procesos estan en la misma maquina entonces pueden comunicarse por medio de una memoria compartida.

### 4. Explique brevemente cómo es el modelo Cliente/Servidor. De un ejemplo de un sistema Cliente/Servidor en la “vida cotidiana” y un ejemplo de un sistema informático que siga el modelo Cliente/Servidor. ¿Conoce algún otro modelo de comunicación?

El modelo cliente/servidor se compone de un host que siempre esta activo que brinda servicios (servidor) y de un proceso que inicia la comunicación con el servidor para acceder a sus servicios (cliente).
Un ejemplo de la vida real puede ser el típico intercambio entre un cliente y un vendedor, en el cual el cliente va a pedir un producto y el vendedor se lo otorga.
Un ejemplo informatico es la Web, un navegador es un proceso cliente y el servidor web es un proceso servidor.

### 5. Describa la funcionalidad de la entidad genérica “Agente de usuario” o “User agent”

Un agente de usuario es una aplicación informática que funciona como cliente en un protocolo de red; el nombre se aplica generalmente para referirse a aquellas aplicaciones que acceden a la World Wide Web.

## HTTP

### 6. ¿Qué son y en qué se diferencian HTML y HTTP?

La principal diferencia entre HTML y HTTP es que HTML es un formato de texto mientras que HTTP es un protocolo de la capa de aplicación. En otras palabras, las paginas web pueden contener archivos HTMl, HTTP va a definir cómo los clientes web solicitan estas paginas a los servidores y cómo los servidores transfieren esas páginas a los clientes.

Cuando un usuario solicita una página web (por ejemplo, haciendo clic en un hipervínculo), el navegador envía al servidor mensajes de solicitud HTTP, pidiendo los objetos contenidos en la página. El servidor
recibe las solicitudes y responde con mensajes de respuesta HTTP que contienen los objetos.

### 7. Utilizando la VM, abra una terminal e investigue sobre el comando curl. Analice para qué sirven los siguientes parámetros (-I, -H, -X, -s)

El comando "curl" nos permite transferir datos desde o hacia un servidor utilizando protocolos. Funciona sin interaccion del usuario y permite acceder a información de envio de mensajes de terminales; por ejemplo, los headers. <br>
Los parametros que se pueden utilizar son:

- -I: muestra el header HTTP del request
- -H: sirve para agregar/modificar información al header del request que se va a enviar
- -X: especifica el método a utilizar en el request
- -s: no muestra mensajes de error

### 8. Ejecute el comando curl sin ningún parámetro adicional y acceda a www.redes.unlp.edu.ar. Luego responda:

### a. ¿Cuántos requerimientos realizó y qué recibió? Pruebe redirigiendo la salida(>) del comando curl a un archivo con extensión html y abrirlo con un navegador.

Se realizó un único request (con el método GET) y se recibió texto plano con formato HTML. Si se abre con un navegador se obtiene una página web.

### b. ¿Cómo funcionan los atributos href de los tags link e img en html?

Los atributos href contienen URL de un atributo, los mismos son vinculos a objetos dentro (img) o fuera (link) de la pagina.
Cuando los navegadores encuentran estos elementos en el archivo HTML hacen una solicitud al servidor para obtenerlos.

### c. Para visualizar la página completa con imágenes como en un navegador, ¿alcanza con realizar un único requerimiento? ¿Cuántos requerimientos serían necesarios para obtener una página que tiene dos CSS, dos Javascript y tres imágenes? Diferencie como funcionaría un navegador respecto al comando curl ejecutado previamente.

No, no es necesario ya que debo hacer un request por cada elemento. Para obtener una página así debo realizar 9 requerimientos:

- 2 por cada CSS
- 2 por cada JS
- 3 por cada imagen
- 1 por el HTML
- 1 por el favicon

Cuando ejecutamos el comando `curl www.redes.unlp.edu.ar` la herramienta curl hará una unica peticion al recurso, mientras que el navegador hará varios request para cargar los distintos recursos de la pagina.

### 9. Ejecute a continuación los siguientes comandos: <i> curl -v -s www.redes.unlp.edu.ar > /dev/null </i> y <i>curl -I -v -s www.redes.unlp.edu.ar</i>

### ¿Qué diferencias nota entre cada uno?

El primer comando esta haciendo un request a la URL con los parametros -v y -s, y redirecciona la respuesta a /dev/null. El segundo comando hace el mismo request, sin redireccionar, pero agregando el parametro -I el cual permite que se visualice el header de la peticion.

### ¿Qué ocurre si en el primer comando quita la redirección a /dev/null? ¿Por qué no es necesaria en el segundo comando?

Si al primer comando se le quita la redireccion muestra, además del headers de la peticion, el contenido de la misma (archivo HTML). En el segundo comando no es necesario redireccionar ya que utilizo el atributo -I, el cual me muestra solo el header de la peticion.

### ¿Cuántas cabeceras viajaron en el requerimiento? ¿Y en la respuesta?

En el requerimiento viajaron 3 cabeceras (Host, User-Agent y Accept) y en la respuesta viajaron 7 (Date, Server, Last-modified, Etag, Accept-Ranges, Content-Length, Content-Type).

### 10. ¿Qué indica la cabecera Date?

La cabecera Date indica la fecha en que se realizó el request.

### 11. En HTTP/1.0, ¿cómo sabe el cliente que ya recibió todo el objeto solicitado completamente? ¿Y en HTTP/1.1?

En HTTP/1.0 la conexión se mantendrá activa hasta que el cliente haya recibido todo el contenido.
En HTTP/1.1 podemos asumir que el cliente recibió todo el objeto debido a dos encabezados:

- `Content-Length`: indica el tamaño del objeto.
- `Connection`: indica si la sesión se mantuvo abierta o se cerro, por lógica si se cerró entonces el cliente recibió todo el objeto.

### 12. Investigue los distintos tipos de códigos de retorno de un servidor web y su significado. Considere que los mismos se clasifican en categorías (2XX, 3XX, 4XX, 5XX).

Los códigos de retorno son:

- 200: Peticiones correctas
- 300: Redirecciones
- 400: Errores del cliente
- 500: Errores del servidor

### 13. Utilizando curl, realice un requerimiento con el método HEAD al sitio www.redes.unlp.edu.ar e indique:

<img src="img\tp2ej13-1.png">

### a. ¿Qué información brinda la primer línea de la respuesta?

La primer línea de respuesta indica: versión HTTP y código de retorno

### b. ¿Cuántos encabezados muestra la respuesta?

La respuesta muestra 7 encabezados.

### c. ¿Qué servidor web está sirviendo la página?

El servidor es: Apache/2.4.53 (Unix)

### d. ¿El acceso a la página solicitada fue exitoso o no?

Si, el acceso fue exitoso ya que el código se respuesta fue 200 OK.

### e. ¿Cuándo fue la última vez que se modificó la página?

La ultima vez que se modifico la pagina fue el 13 de Abril de 2022.

### f. Solicite la página nuevamente con curl usando GET, pero esta vez indique que quiere obtenerla sólo si la misma fue modificada en una fecha posterior a la que efectivamente fue modificada. ¿Cómo lo hace? ¿Qué resultado obtuvo? ¿Puede explicar para qué sirve?

Para realizar este requerimiento utilizo el atributo -z, la linea de comando final me quedaria: `curl -z 'Sun, 28 Aug 2022' www.redes.unlp.edu.ar`. <br>
Otra opción es utilizar el header `If-Modified-Since:` al cual se le tiene que asignar una fecha (la comparación es menor estricto) y en base a esa fecha se evalua si el archivo fue modificado desde esa fecha. Las respuestas pueden ser:

- Si le pasamos una fecha anterior a la última fecha de modificación, obtenemos la misma respuesta.
- Si le pasamos una fecha igual o posterior, obtenemos una respuesta con el estado 304 Not Modified.

### 14. Utilizando curl, acceda al sitio www.redes.unlp.edu.ar/restringido/index.php y siga las instrucciones y las pistas que vaya recibiendo hasta obtener la respuesta final. Será de utilidad para resolver este ejercicio poder analizar tanto el contenido de cada página como los encabezados.

Paso 1: `curl http://www.redes.unlp.edu.ar/restringido/index.php`
<img src="img\tp2ej14.png">

Paso 2: `curl www.redes.unlp.edu.ar/obtener-usuario.php`
<img src="img\tp2ej142.png">

Paso 3: `curl -H 'Usuario-Redes: obtener' www.redes.unlp.edu.ar/obtener-usuario.php`
<img src="img\tp2ej143.png">

Paso 4: `curl -H "Authorization: Basic $(echo -n redes:RYC | base64)" http://www.redes.unlp.edu.ar/restringido/index.php`
<img src="img\tp2ej144.png">

Paso 5: `curl -H "Authorization: Basic $(echo -n redes:RYC | base64)" -I http://www.redes.unlp.edu.ar/restringido/index.php `
<img src="img\tp2ej145.png">

Paso 6: `curl -H "Authorization: Basic $(echo -n redes:RYC | base64)" http://www.redes.unlp.edu.ar/restringido/the-end.php `
<img src="img\tp2ej146.png">

### 15. Utilizando la VM, realice las siguientes pruebas:

### a. Ejecute el comando ’curl www.redes.unlp.edu.ar/extras/prueba-http-1-0.txt’ y copie la salida completa (incluyendo los dos saltos de linea del final).

### b. Desde la consola ejecute el comando telnet www.redes.unlp.edu.ar 80 y luego pegue el contenido que tiene almacenado en el portapapeles. ¿Qué ocurre luego de hacerlo?

<img src="img\tp2ej15b.png">

### c. Repita el proceso anterior, pero copiando la salida del recurso /extras/prueba-http-1-1.txt. Verifique que debería poder pegar varias veces el mismo contenido sin tener que ejecutar telnet nuevamente.

Copiando la salida del recurso la salida es la misma con la diferencia que puedo pegar varias veces el mismo contenido sin tener que ejecutar el comando telnet nuevamente.

### 16. En base a lo obtenido en el ejercicio anterior, responda:

### ¿Qué está haciendo al ejecutar el comando telnet?

Telnet permite el control remoto de los ordenadores por medio de entradas y salidas basadas en texto. Con este objetivo, se crea una conexión cliente-servidor a través del protocolo TCP y del puerto TCP 23, donde el dispositivo controlado ejerce de servidor y espera a los comandos pertinentes.

### ¿Qué método HTTP utilizó? ¿Qué recurso solicitó?

Utilizó el método ` GET` y solicitó el recurso `/http/HTTP-1.x/`.

### ¿Qué diferencias notó entre los dos casos? ¿Puede explicar por qué?

La principal diferencia que encontré es que en el primer caso, usando HTTP 1.0, luego de obtener una respuesta la conexión se cierra inmediatamente; mientras que con el protocolo HTTP 1.1 la conexión se mantiene abierta por unos segundos, permitiendo enviar nuevas peticiones.

### ¿Cuál de los dos casos le parece más eficiente? Piense en el ejercicio donde analizó la cantidad de requerimientos necesarios para obtener una página con estilos, javascripts e imágenes. El caso elegido, ¿puede traer asociado algún problema?

Considero que HTTP 1.1 es más eficiente debido a que puedo mandar un request varias veces sin tener que abrir nuevamente la conexión.

### 17. En el siguiente ejercicio veremos la diferencia entre los métodos POST y GET. Para ello, será necesario utilizar la VM y la herramienta Wireshark. Antes de iniciar considere: (puntos a considerar)

### c. Utilizando el analizador de paquetes Wireshark capture los paquetes enviados y recibidos al presionar el botón Enviar.

GET:
<img src="img\tp2ej17GET.png">

POST:
<img src="img\tp2ej17POST.png">

### d. ¿Qué diferencias detectó en los mensajes enviados por el cliente?

El cliente permite enviar un formulario por el metodo GET y POST.
La principal diferencia es que en el GET los mensajes se envian por el URL mientras que en el POST los mensajes se envian en el body de la peticion.

### e. ¿Observó alguna diferencia en el browser si se utiliza un mensaje u otro?

Como GET hace uso de la URL para transferir los parámetros, estos son posibles de observar desde el navegador. En cambio como POST hace uso del cuerpo del request para el envio de los parámetros, estos no estan visibles a simple vista desde el navegador.

### 18. Investigue cuál es el principal uso que se le da a las cabeceras Set-Cookie y Cookie en HTTP y qué relación tienen con el funcionamiento del protocolo HTTP.

La cabecera de respuesta HTTP `Set-Cookie` se usa para enviar cookies desde el servidor al agente de usuario, así el agente de usuario puede enviarlos de vuelta al servidor.
La cabecera `Cookie` contiene los cookies que el User Agent desea enviar al servidor en un mensaje.
Estas cabeceras ayuda a manejar las cookies del protocolo HTTP. Una cookie HTTP, cookie web o cookie de navegador es una pequeña pieza de datos que un servidor envía a el navegador web del usuario. El navegador guarda estos datos y los envía de regreso junto con la nueva petición al mismo servidor. Las cookies se usan generalmente para decirle al servidor que dos peticiones tienen su origen en el mismo navegador web lo que permite, por ejemplo, mantener la sesión de un usuario abierta. Las cookies permiten recordar la información de estado en vista a que el protocolo HTTP es un protocolo sin estado.

### 19. ¿Cuál es la diferencia entre un protocolo binario y uno basado en texto? ¿de que tipo de protocolo se trata HTTP/1.0, HTTP/1.1 y HTTP/2?

Un protocolo basado en texto es un protocolo de comunicación cuya representación de contenido está en formato legible por humanos
Un protocolo binario es un protocolo de comunicación que utiliza todos los valores de un byte, a diferencia del protocolo basado en texto que solo usa valores correspondientes a caracteres legibles por humanos en codificación ASCII. Los protocolos binarios están pensados ​​para ser leídos por una máquina en lugar de un ser humano. Los protocolos binarios tienen la ventaja de la concisión, que se traduce en velocidad de transmisión e interpretación.

HTTP/1.0 y HTTP/1.1 usan protocolo basado en texto mientras que HTTP/2 usa protocolo binario.

### 20. Analice de que se tratan las siguientes características de HTTP/2: stream, frame, server-push

El <b>stream</b> es el intercambio bidireccional de datos de una conexión HTTP establecida, que puede llevar uno o más mensajes.
Un mensaje es un conjunto de <b>frames</b>. <b>Frame</b> es el patrón de comunicación más pequeño en HTTP/2, cada frame tiene un encabezado para identificar a la secuencia a la que pertenece para después formar un mensaje lógico.
<br>
<b>Server Push</b> permite adelantar la carga de los recursos para que se descarguen al mismo tiempo que el HTML, evitando así que el navegador tenga que pedirlos después de descargar y analizar el HTML.

### 21. Responder las siguientes preguntas:

### a. ¿Qué función cumple la cabecera Host en HTTP 1.1? ¿Existía en HTTP 1.0? ¿Qué sucede en HTTP/2?

La cabecera `Host` especifica el nombre de dominio del servidor, y opcionalmente el número de puerto TCP en el que el servidor esta escuchando; si no se provee un puerto se usará el puerto por defecto. En HTTP/1.1 se debe enviar obligatoriamente, mientras que en HTTP/1.0 no era requerido. <br>
En HTTP/2 el header `Host` se cambió por `authority`, quien contiene la autoridad de la URI destino.

### b. ¿Cómo quedaría en HTTP/2 el siguiente pedido realizado en HTTP/1.1 si se está usando https?

```
GET /index.php HTTP/1.1
Host: www.info.unlp.edu.ar
```

Esta peticion quedaria:

```
:method GET
:path /index.php
:scheme https
:authority www.info.unlp.edu.ar
```
