## Práctica 1 - Introducción

### 1.¿Qué es una red? ¿Cuál es el principal objetivo para construir una red?

Una red es un conjunto de dispositivos interconectados. El principal objetivo de una red es compartir recursos: dispositivos, información o servicios.


### 2.¿Qué es Internet? Describa los principales componentes que permiten su funcionamiento.

Internet es una red de computadoras descentralizada y publica que usa el protocolo TCP/IP. Los principales componentes son la red, los usuarios y los clientes. Su modelo es hourglass.


### 3.¿Qué son las RFCs?

RFC son una serie de pautas o convenciones para determinar cómo deberian funcionar los protocolos.


### 4.¿Qué es un protocolo?

Son un conjunto de reglas que se tienen que seguir para que una comunicación entre dos componentes que estan conectados a una red sea exitosa.


### 5.¿Por qué dos máquinas con distintos sistemas operativos pueden formar parte de una misma red?

Dos maquinas pueden comunicarse siempre y cuando sigan el mismo protocolo de red.


### 6.¿Cuáles son las 2 categorías en las que pueden clasificarse a los sistemas finales o End Systems? Dé un ejemplo del rol de cada uno en alguna aplicación distribuida que corra sobre Internet.

Las dos categorías son: cliente y servidor. Un ejemplo del rol del lado del servidor es: un servidor Web y del lado del cliente un browser.


### 7.¿Cuál es la diferencia entre una red conmutada de paquetes de una red conmutada de circuitos?

La diferencia entre una red conmutada de paquetes de una red conmutada de circuitos es que la de paquetes es más eficiente porque permite varias conexiones a la vez mientras que en una red de circuitos la conexión es uno a uno y el circuito queda completamente ocupado hasta que se corte la comunicación.


### 8.Analice qué tipo de red es una red de telefonía y qué tipo de red es Internet.

Una red de telefonía es una red conmutada de circuitos. Internet es una red conmutada de paquetes.


### 9.Describa brevemente las distintas alternativas que conoce para acceder a Internet en su hogar.

Un proveedor me otorga Intenet (puede ser por router o por cable) recibiendola exteramente por fibra optica, cable coaxial, etc.


### 10.¿Qué ventajas tiene una implementación basada en capas o niveles?


Una implementación basada en capas es escalable, tiene mayor seguridad ya que puedo proteger a capas inferiores, es modularizable.


### 11.¿Cómo se llama la PDU de cada una de las siguientes capas: Aplicación, Transporte, Red y Enlace?


La PDU es Protocol Data Unit, es decir, define el tipo de mensaje que se enviara en esa capa.
1. Aplicacion: mensajes
2. Transporte: segmentos
3. Enlace: datagrama
4. Red: trama
5. Fisica: bit


### 12.¿Qué es la encapsulación? Si una capa realiza la encapsulación de datos, ¿qué capa del nodo receptor realizará el proceso inverso?

La encapsulacion es el mensaje agregado de cada capa al mensaje de la capa anterior, es decir, se le va agregando información a medida que va bajando por las capas. El proceso inverso lo realizará la misma capa que encapsulo el mensaje original.


### 13.Describa cuáles son las funciones de cada una de las capas del stack TCP/IP o protocolo de Internet.

Las capas de TCP/IP son:

1. Aplicacion: es la capa con mayor nivel de abstracción. Es aquella a la que accede el usuario. Esta capa incluye muchos protocolos, como el protocolo HTTP (el cual provee servicios para peticiones de documentos Web y transferencias, y FTP (el cual se utiliza para la transferencia de archivos entre dos sistemas finales). Otro ejemplo de protocolo que se ubica en esta capa es el de DNS, el cual sirve para traducir nombres de dominio.

2. Transporte: es la capa encargada de transmitir los mensajes de la capa de aplicación de una computadora a otra. Los protocolos que utiliza son: UDP y TCP

3. Red: La capa de red es responsable de mover paquetes de la capa de red, conocidos como datagramas, de un host a otro. El protocolo de la capa de transporte (TCP o UDP) en un host fuente, pasa un segmento de la capa de transporte y una dirección de destino a la capa de red. La capa de red luego provee el servicio de distribuir el segmento a la capa de transporte en el bost destino.

4. Enlace: La capa de red rutea un datagrama a través de una serie de routers entre el origen y el destino. Para mover un paquete de un nodo (host o router) al siguiente nodo en la ruta, la capa de red depende de los servicios de la capa de enlace. En particular, en cada nodo, la capa de red pasa el datagrama a la capa de enlace, la cual distribuye el datagrama al siguiente nodo a lo largo de la ruta. En este siguiente nodo, la capa de enlace pasa el datagrama a la capa de red.

5. Fisica: Mientras que el trabajo de la capa de enlace es mover frames enteros de un elemento de red a otro adyacente, el trabajo de la capa fisica es mover los bits individuales que están dentro del frame de un nodo al próximo. Los protocolos en esta capa son dependientes al enlace y por ende también del medio actual de transición del enlace (por ejemplo cable de cobre, fibra óptica, etc).


### 14.Compare el modelo OSI con la implementación TCP/IP.

Ambos son sistemas en capas que utilizan conmutacion de paquetes. Las capas son similares pero TCP/IP combina algunas de las capas del modelo OSI en una sola capa. TCP/IP tiene 5 y OSI tiene 7.
