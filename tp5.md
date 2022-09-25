## Práctica 5 - Capa de Transporte - Parte I

### 1. ¿Cuál es la función de la capa de transporte?

La función de la capa de transporte es conectar procesos de la capa de aplicación. Tiene dos posibles modelos, acompañados del protocolo de internet (IP), UDP y TCP. Siendo UDP el menos confiable ya que trabaja bajo el mismo lema de _best effort_ que IP, por lo tanto no tiene un sistema muy complejo de detección y control de errores, el cual TCP si tiene, además de control de flujo y de congestión.

### 2. Describa la estructura del segmento TCP y UDP.

La estructura de UDP consta de una cabecera y de los datos de la aplicación. Las cabeceras son:

- _Número de puerto de origen_ y _número de puerto de destino_: Los numeros de puerto permiten al host de destino pasar los datos de la aplicación al proceso apropiado que está ejecutandose en el sistema terminal de destino.
- _Longitud_: especifica el numero de bytes del segmento (cabecera + datos)
- _Suma de comprobación_: se utiliza para evaluar posibles errores del segmento.  
  <br>

Por otro lado, la estructura de un segmento TCP es mucho más compleja. El segmento TCP consta de campos de cabecera y un campo de datos. Al igual que con UDP, la cabecera incluye los números de puerto de origen y de destino, que se utilizan para multiplexar y
demultiplexar los datos de y para las aplicaciones de la capa superior. También, al igual que UDP, la cabecera incluye un campo de suma de comprobación. La cabecera de un segmento TCP también
contiene los siguientes campos:

- _Número de secuencia_ y _número de reconocimiento_: son utilizados por el emisor y el receptor de TCP para implementar un servicio de
  transferencia de datos fiable.
- _Ventana de recepción_: se utiliza para el control de flujo.
- _Longitud de cabecera_: especifica la longitud de la cabecera TCP en palabras de 32 bits.
- _Opciones_: es opcional y de longitud variable.
- _Campo indicador_: tiene 6 bits. Los indicadores son: ACK, RST, SYN, FIN, PSH y URG.
- _Puntero de datos urgentes_

### 3. ¿Cuál es el objetivo del uso de puertos en el modelo TCP/IP?

El objetivo de utilizar puertos en el modelo TCP/IP es diferenciar los distintos procesos dentro del mismo nodo terminal para identificar emisoires y receptores. Esto resulta fundamental para que se puede establecer la comunicación entre cliente y servidor.

### 4. Compare TCP y UDP en cuanto a:

### a. Confiabilidad.

| UDP                                                                                                                               | TCP                                                                                                                                                                                                                               |
| --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| No es fiable.                                                                                                                     | Es fiable ya que usa técnicas de control de flujo, números de secuencia, temporizadores y mensajes de reconocimiento.                                                                                                             |
| No garantiza que los segmentos lleguen al proceso destino, tampoco que lleguen en orden o se conserve la integridad de los datos. | Garantiza que los datos transmitidos por el proceso emisor sean entregados al proceso receptor, correctamente y en orden. Continuará reenviando un segmento hasta que la recepción del mismo haya sido confirmada por el destino. |

### b. Multiplexación.

| UDP                                                                                                                                                                                                                                               | TCP                                                                                                                                                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Utiliza multiplexación y demultiplexación SIN conexión.                                                                                                                                                                                           | Utiliza multiplexación y demultiplexación orientada a la conexión.                                                                                                                                                                                   |
| Creamos sockets indicando el número de puerto.                                                                                                                                                                                                    | El socket, en TCP se identifica por una tupla de cuatro elementos: Dirección IP Origen, Nro. Puerto Origen, Dirección IP Destino, Nro. Puerto Destino.                                                                                               |
| El segmento (de UDP + IP) identifica el socket destino mediante dos campos de cabecera: Dirección IP Destino y Nro. Puerto Destino. Ademas el segmento tiene una “dirección de retorno”. Por si el receptor desea devolver un segmento al emisor. | Dos segmentos TCP entrantes con direcciones IP de origen o números de puerto de origen diferentes (con la excepción de un segmento TCP que transporte la solicitud original de establecimiento de conexión) serán dirigidos a dos sockets distintos. |
| Cabeceras de 8 bytes.                                                                                                                                                                                                                             | Cabecera de 20 bytes (es variable).                                                                                                                                                                                                                  |

### c. Orientado a la conexión.

| UDP                                                                                                                                                                                    | TCP                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| Es un protocolo sin conexión. No tiene lugar una fase de establecimiento de la conexión entre las entidades de la capa de transporte emisora y receptora previa al envío del segmento. | Lleva a cabo un proceso de establecimiento de la conexión en tres fases antes de iniciar la transferencia de datos. |
| No mantiene información del estado de la conexión.                                                                                                                                     | Mantiene información acerca del estado de la conexión en los sistemas terminales.                                   |
| Suele soportar más clientes activos cuando la aplicación se ejecuta sobre UDP.                                                                                                         | La conexión proporciona un servicio full-duplex.                                                                    |
|                                                                                                                                                                                        | La conexión es punto a punto.                                                                                       |
|                                                                                                                                                                                        | Cada lado de la conexión tiene su propio buffer de emisión y su propio buffer de recepción.                         |
|                                                                                                                                                                                        | Cada host tiene un conjunto de buffers, variables y un socket de conexión.                                          |

### d. Controles de congestión.

| UDP                                  | TCP                                                                                                                                                                                                                                                                                                                                   |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| No implementa control de congestión. | Dispone de un mecanismo de control de congestión que regula el flujo del emisor TCP de la capa de transporte cuando uno o más de los enlaces existentes entre los hosts de origen y de destino están excesivamente congestionados.                                                                                                    |
|                                      | Proporciona un servicio de control de flujo a sus aplicaciones para eliminar la posibilidad de que el emisor desborde el buffer del receptor. Por lo tanto, un servicio de adaptación de velocidades (adapta la velocidad a la que el emisor está transmitiendo frente a la velocidad a la que la aplicación receptora está leyendo). |
|                                      | El emisor dispone (y determina el tamaño) de una ventana de recepción. Se emplea para proporcionar al emisor una idea de cuánto espacio libre hay disponible en el buffer del receptor. Debido a que la conexión es full dúplex, cada proceso dispone de una ventana de recepción diferente.                                          |

### e. Utilización de puertos.

| UDP                                                                                    | TCP                                                                                                                                                                                                                                                             |
| -------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| El socket está definido por el número de puerto destino y la dirección IP del destino. | El socket está definido para cada extremo de la conexión. Es decir, por los cuatro campos (IPOrigen, PuertoOrigen, IPDestino, PuertoDestino). Esto quiere decir que por cada socket pueden intercambiar datos únicamente dos procesos (conexión punto a punto). |
| Muchos clientes pueden enviar datos por un mismo socket.                               |                                                                                                                                                                                                                                                                 |

### 5. La PDU de la capa de transporte es el segmento. Sin embargo, en algunos contextos suele utilizarse el término datagrama. Indique cuando.

Se usa cuando pasa a la capa de red.

### 6. Describa el saludo de tres vías de TCP. ¿Se utiliza algo similar en UDP?

_Explicar el saludo, creo que es el del SYN_
En UDP no se utiliza ya que no establece una conexión entre procesos.
