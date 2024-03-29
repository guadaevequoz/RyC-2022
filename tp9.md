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

**Procedimiento:**

1. Tomo el primer octeto del hexa y lo paso a binario: `00` --> `0000 0000`.
2. Invertir el septimo bit: `0000 0000` --> `0000 0010`
3. Convertir de binario a decimal: `0000 0010` --> `2`
4. Reemplazar el primer octeto con el decimal: `00:1b:77:b1:49:a1` --> `2:1b:77:b1:49:a1`
5. Agregar _ff:fe_ a la mitad de la direccion: `2:1b:77:b1:49:a1` --> `2:1b:77: ff:fe: b1:49:a1`
6. Agregar _fe80::_ al comienzo: `2:1b:77: ff:fe: b1:49:a1` --> `fe80::2:1b:77:ff:fe:b1:49:a1`
7. La ordeno: `fe80::2:1b:77:ff:fe:b1:49:a1` --> `fe80::21b:77ff:feb1:49a1`

El resultado es: `fe80::21b:77ff:feb1:49a1`

- _e8:1c:23:a3:21:f4_:

1. Tomo el primer octeto del hexa y lo paso a binario: `e8` --> `1110 1000`.
2. Invertir el septimo bit: `1110 1000` --> `1110 1010`
3. Convertir de binario a decimal: `1110 1010` --> `234`
4. Reemplazar el primer octeto con el decimal: `e8:1c:23:a3:21:f4` --> `234:1c:23:a3:21:f4`
5. Agregar _ff:fe_ a la mitad de la direccion: `234:1c:23:a3:21:f4` --> `234:1c:23: ff:fe: a3:21:f4`
6. Agregar _fe80::_ al comienzo: `234:1c:23: ff:fe: a3:21:f4` --> `fe80::234:1c:23:ff:fe:a3:21:f4`
7. La ordeno y paso el 234 a hexa: `fe80::ea:1c:23:ff:fe:a3:21:f4` --> `fe80::ea1c:23ff:fea3:21f4`

El resultado es: `fe80::ea1c:23ff:fea3:21f4`

### 8. ¿Cuál de las siguientes direcciones IPv6 no son válidas?

- _2001:0:1019:afde::1_: Es válida. La direccion original es: `2001:0:1019:afde:0:0:0:1`.
- _2001::1871::4_: No es válida ya que la abreviatura `::` puede repetirse una sola vez en una dirección.
- _3ffg:8712:0:1:0000:aede:aaaa:1211_: No es válida ya que `g` no pertenece a los valores hexadecimales.
- _3::1_: Es válida. La direccion original es: `3:0:0:0:0:0:0:1`.
- _::_: Es válida (creo que es una por default).
- _2001::_: Es válida. La direccion original es: `2001:0:0:0:0:0:0:0`.
- _3ffe:1080:1212:56ed:75da:43ff:fe90:affe_: Es válida.
- _3ffe:1080:1212:56ed:75da:43ff:fe90:affe:1001_: No es válida ya que contiene un grupo de 16 bits demás.

### 9. ¿Cuál sería una abreviatura correcta de 3f80:0000:0000:0a00:0000:0000:0000:0845?

Las abreviatura correcta es: `3f80:0:0:a00::845`.

### 10. Indique si las siguientes direcciones son de link-local, global-address, multicast, etc.

Las _link-local_ tienen 10 bits de red, 54 bits 0 y 64 bits de IID. El prefijo asignado es `FE80::/10` y el utilizado es `FE80::/64`.
Las _site-local_ tienen 10 bits de red, 54 bits de site Id y 64 bits de IID. El prefijo `FEC0::/10`. Similar a las redes privadas de IPv4.
Las _unique-local_ tienen 48 bits de unique Id, 16 bits de site Id y 64 bits de IID. El prefijo asignado es `FC00::/7` y el utilizado es `FD00::/8`. Reemplazan las direcciones de Site Local.
Las _global-address_ tienen 48 bits de provideer, 16 bits de site Id y 64 bits de host. El prefijo asignado es cedido por un provider. Es de alcance de internet.
Las _multicast-address_ tienen 16 bits de configuracion (flags y scope) y 112 bits de group ID. El prefijo `FF00::/8`.

- _fe80::1/64_: `link-local`
- _3ffe:4543:2:100:4398::1/64_: `global-address`
- _::_: `anycast`
- _::1_: `anycast`
- _ff02::2_:`multicast`
- _2818:edbc:43e1::8721:122_: `global-address`
- _ff02::9_:`multicast`

### 11. Dado el siguiente diagrama, ¿qué direcciones IPv6 será capaz de autoconfigurar el nodo A en cada una de sus interfaces?

<img src="img/tp9-ej11-enunciado.png">

- Primero genera `fe80::21b:77ff:feb1:49a1` (link-local)
- Luego genera `fe80::c225:eeff:feba:93e1` (link-local)

### 12. Al autogenerarse una dirección IPv6 sus últimos 64 bits en muchas ocasiones no se deducen de la dirección MAC, se generan de forma random, ¿por qué sucede esto? ¿Qué es lo que se intenta evitar? (Ver direcciones temporarias, RFC 8981)

Una dirección temporal IPv6 emplea un número de 64 bits generado aleatoriamente como ID de interfaz, en lugar de la dirección MAC de la interfaz. Puede utilizar direcciones temporales para cualquier interfaz de un nodo de IPv6 que desee mantener anónimo. Por ejemplo, puede utilizar direcciones temporales para las interfaces de un host que deba acceder a servidores web públicos. Las direcciones temporales implementan mejoras de privacidad de IPv6.

### 13. Utilizando la máquina virtual abrir la topología llamada 3-ruteo-OSPF.imn para realizar las siguientes pruebas:

Para realizar el ejercicio tuve que copiar el código que esta en el LINTI y pasarlo a un archivo y guardarlo con la extensión `.imn`.

### a. Habilitar la vista de las direcciones IPv6 en la topología (View ->show ->IPv6 Addresses).

?? no me muestra nada

### b. Esperar a que la red converja. Verificar, mediante ping6, la comunicación entre n6 y n7.

?? no me deja comunicarme

### c. Observar la configuración IPv6:

### i. De la PC n6.

### ii. De la PC n7.

### iii. Del router n1.

### iv. La tabla de rutas tanto de las PCs como de los routers.

### d. Responda:

### i. ¿Cuántas direcciones IPv6 se observan tanto en la PC n6 como en la PC n7?

### ii. ¿Es posible desde la PC n7 hacer un ping6 a cada una de las direcciones IPv6 de la PC n6 ¿Por qué?

### e. Cuando se quiere hacer ping6 a una dirección link-local es necesario especificar la interfaz que se quiere utilizar (ping6 -I eth0 <IPv6-address>) ¿Por qué?

### f. Deshabilite la configuración de IPv6 en la PC n7 mediante el comando: sysctl -w net.ipv6.conf.all.disable_ipv6=1

### i. Verifique las IPs configuradas en la PC.

### ii. Luego de deshabilitarse IPv6, ¿puede comunicarse con la PC n6? ¿Cómo?
