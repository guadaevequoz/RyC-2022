## Práctica 9 - Capa de Red - IPv6

## IPv6

### 1. ¿Qué es IPv6? ¿Por qué es necesaria su implementación?

IPv6 surge de la necesidad de más direcciones de red ya que con IPv4 no nos alcanzaba. Para responder a esta necesidad de un espacio de direcciones IP más grande, se desarrolló un nuevo protocolo IP, el protocolo IPv6. Los diseñadores de IPv6 también aprovecharon la oportunidad para ajustar y expandir otros aspectos de IPv4, basándose en la experiencia acumulada sobre el funcionamiento de dicho protocolo.

El formato del datagrama IPv6 cambio con respecto del de IPv4:

- Tiene una cabecera de de 40 bytes simplificada. Algunos de los campos de IPv4 se han eliminado o se han hecho opcionales. La cabecera resultante, con una longitud fija de 40 bytes, permite un procesamiento más rápido del datagrama IP en los routers. Una nueva codificación de las opciones permite un procesamiento más flexible de las mismas.
- Capacidades ampliadas de direccionamiento. IPv6 aumenta el tamaño de la dirección IP, de 32 a 128 bits. De esta manera, se asegura que el mundo no se quedará sin direcciones IP. Además de las direcciones de unidifusión y de multidifusión, IPv6 ha introducido un nuevo tipo de dirección, denominado dirección anycast, que permite entregar un datagrama a uno cualquiera de un grupo de hosts.
- Etiquetado del flujo. IPv6 utiliza una definición bastante amplia de flujo. El documento RFC 2460 establece que esto permite “etiquetar los paquetes que pertenecen a determinados flujos para los que el emisor solicita un tratamiento especial, como una calidad de servicio no predeterminada o un servicio en tiempo real”. Por ejemplo, la transmisión de audio y de vídeo puede posiblemente tratarse como un flujo. Por el contrario, aplicaciones más tradicionales, como la transferencia de archivos y el correo electrónico, podrían no tratarse como flujos.

En IPv6 se definen los siguientes campos:

- _Versión_. Este campo de 4 bits identifica el número de versión IP. Nada sorprendentemente, IPv6 transporta un valor de 6 en este campo. Observe que incluir en este campo el valor 4 no implica que se cree un datagrama IPv4 válido.
- _Clase de tráfico_. Al igual que el campo TOS de IPv4, el campo de clase de tráfico, de 8 bits, puede utilizarse para dar prioridad a ciertos datagramas dentro de un flujo, o para dar prioridad a los datagramas de determinadas aplicaciones (por ejemplo, Voz sobre IP) frente a los datagramas de otras aplicaciones (por ejemplo, correo electrónico SMTP).
- _Etiqueta de flujo_. Como hemos mencionado anteriormente, este campo de 20 bits se utiliza para identificar un flujo de datagramas.
- _Longitud de la carga útil_. Este valor de 16 bits se trata como un entero sin signo que proporciona el número de bytes del datagrama IPv6 incluidos a continuación de la cabecera del datagrama, que es de 40 bytes y tiene longitud fija.
- _Siguiente cabecera_. Este campo identifica el protocolo (por ejemplo, TCP o UDP) al que se entregará el contenido (el campo de datos) de este datagrama. El campo utiliza los mismos valores que el campo de protocolo de la cabecera IPv4.
- _Límite de saltos_. Cada router que reenvía un datagrama decrementa el contenido de este campo en una unidad. Si el límite de saltos alcanza el valor cero, el datagrama se descarta.
- _Direcciones de origen y de destino_. Los distintos formatos de la dirección de 128 bits de IPv6 se describen en el documento RFC 4291.
- _Datos_. Esta es la parte de la carga útil del datagrama IPv6. Cuando el datagrama llegue a su destino, la carga útil se extraerá del datagrama IP y se pasará al protocolo especificado en el campo Siguiente cabecera.

### 2. ¿Por qué no es necesario el campo Header Length en IPv6?

El campo Header Length era necesario en IPv4 ya que la cabecera podía tener un tamaño variable, en IPv6 esto no sucede ya que la cabecera tiene un tamaño fijo.

### 3. ¿En qué se diferencia el checksum de IPv4 e IPv6? Y en cuánto a los campos checksum de TCP y UDP, ¿sufren alguna modificación en cuanto a su obligatoriedad de cálculo?

Puesto que los protocolos de la capa de transporte (por ejemplo, TCP y UDP) y de la capa de enlace de datos (por ejemplo, Ethernet) de Internet utilizan sumas de comprobación, los diseñadores de IP probablemente pensaron que esta funcionalidad ya era suficientemente redundante en la capa de red y podía eliminarse. Una vez más, el procesamiento rápido de los paquetes IP era la preocupación principal. Como la cabecera de IPv4 contiene un campo TTL (similar al campo de límite de saltos de IPv6), la suma de comprobación de la cabecera IPv4 necesitaba ser recalculada en cada router. Al igual que la fragmentación y el reensamblado, esta también era una operación muy costosa en IPv4.

### 4. ¿Qué sucede con el campo Opciones en IPv6? ¿Existe, en IPv6, algún forma de enviar información opcional?

El campo opciones en IPv6 se elimina. La cabecera IP estándar ya no incluye un campo de opciones. Sin embargo, las opciones no han desaparecido. En su lugar, el campo de opciones es una de las posibles siguientes cabeceras a las que se apunta desde dentro de la cabecera IPv6. Es decir, al igual que las cabeceras de los protocolos TCP o UDP pueden ser la siguiente cabecera dentro de un paquete IP, también puede serlo un campo de opciones. La eliminación del campo de opciones dio como resultado una cabecera IP de 40 bytes de longitud fija.

### 5. Si quisiese que IPv6 soporte una nueva funcionalidad, ¿cómo lo haría?

Lo agregaria como una opcion al campo de Siguiente Cabecera **CONSULTAR**.

### 6. ¿Es necesario el protocolo ICMP en IPv6? ¿Cumple las mismas funciones que en IPv4?

Los mensajes de ICMP no son obligatorios y, a menudo, no se permiten dentro de una red por razones de seguridad. El protocolo ICMP está disponible tanto para IPv4 como para IPv6. El protocolo de mensajes para IPv4 es ICMPv4. ICMPv6 proporciona estos mismos servicios para IPv6, pero incluye funcionalidad adicional.

ICMPv6 introduce algunas simplificaciones en el envío de mensajes con respecto a ICMPv4, eliminando tipos de mensajes obsoletos que estaban en desuso. Los mensajes ICMPv6 se agrupan en dos tipos o clases: mensajes de error y mensajes informativos. Los mensajes de error tienen cero en el bit de mayor peso del campo Tipo, por lo que sus valores se sitúan entre 0 y 127. Los valores de los mensajes informativos oscilan entre 128 y 255.

Los mensajes de error de ICMPv6, que son similares a los mensajes de error de ICMPv4, se dividen en 4 categorías: destino inaccesible, paquete demasiado grande, tiempo excedido y problemas de parámetros.

Los mensajes informativos de ICMPv6 se subdividen en tres grupos: mensajes de diagnóstico, mensajes para la administración de grupos multidifusión (multicast) (sustituyen a IGMP que se utilizaba para intercambiar información entre encaminadores IP acerca de su estado, y mensajes de Neighbor Discovery (que entre otras funciones sustituye a ARP)

Por razones de seguridad, las cabeceras ICMPv6 pueden ser autenticadas y encriptadas, usando la cabecera correspondiente. El uso de este mecanismo permite, además la prevención de ataques ICMP de negación de Servicio (DoS o Denial of Service Attack), como el conocido ping de la muerte.

### 7. Transforme las siguientes direcciones MACs en Identificadores de Interfaces de 64 bits.

- _00:1b:77:b1:49:a1_:
- _e8:1c:23:a3:21:f4_:
