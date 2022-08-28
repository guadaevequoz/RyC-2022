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

Para realizar este requerimiento utilizo el atributo -z, la linea de comando final me quedaria: `curl -z 'Sun, 28 Aug 2022' www.redes.unlp.edu.ar`

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
