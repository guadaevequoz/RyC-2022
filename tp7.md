## Práctica 7 - Capa de Red - Direccionamiento

## Introducción

### 1. ¿Qué servicios presta la capa de red? ¿Cuál es la PDU en esta capa? ¿Qué dispositivo es considerado sólo de la capa de red?

La capa de red proporciona servicios de _reenvio_ y _enrutamiento_ de paquetes entre diferentes hosts. Esta capa recibe un segmento de la capa de transporte, lo encapsula en un datagrama y lo envia a un host receptor el cual recibira el datagrama y enviará los datos a la capa de transporte.

El PDU de esta capa es el _datagrama_.

El _router_ es el dispositivo es considerado sólo de la capa de red. El router no implementa capas superior a la capa de red. Cada router tiene una tabla de reenvio.

### 2. ¿Por qué se lo considera un protocolo de mejor esfuerzo?

La capa de red de Internet proporciona un servicio de _best-effort_, esto indica que el servicio no asegura la temporización relativa entre paquetes, tampoco está garantizado que los paquetes se reciban en el orden que fueron emitidos y tampoco se garantiza la entrega de los paquetes transmitidos. Por tanto, teniendo en cuenta esta definición, una red que no entregara los paquetes al destino satisfaría la definición de servicio de entrega de mejor esfuerzo. Por ende, se puede decir que un servicio de mejor esfuerzo no proporciona ningun servicio en absoluto.

### 3. ¿Cuántas redes clase A, B y C hay? ¿Cuántos hosts como máximo pueden tener cada una?

| Clase A                     | Clase B                  | Clase C                    |
| --------------------------- | ------------------------ | -------------------------- |
| Cantidad de redes: 126      | Cantidad de redes: 16384 | Cantidad de redes: 2097152 |
| Cantidad de hosts: 16777214 | Cantidad de hosts: 65634 | Cantidad de hosts: 254     |

### 4. ¿Qué son las subredes? ¿Por qué es importante siempre especificar la máscara de subred asociada?

Las subredes surgen cuando una red se vuelve muy grande. El concepto de máscara indica en una dirección IP qué bits son de red y qué bits son de host. Con el uso de redes con clases, la máscara estaba implícita en la dirección de clase, ya que se conocía a priori los bits para red y los bits para host. Cuando se creó el concepto de subredes también se les asoció una máscara de subred, que resultó de utilizar algunos bits de hosts para crear subredes y de esta manera obtener varias subredes con menos hosts cada una.

### 5. ¿Cuál es la finalidad del campo Protocol en la cabecera IP? ¿A qué campos de la capa de transporte se asemeja en su funcionalidad?

El campo _Protocol_ solo se suele emplear cuando un datagrama IP alcanza su destino final. El valor de este campo indica el protocolo específico de la capa de transporte al que se pasarán los datos contenidos en ese datagrama IP. Por ejemplo, un valor de 6 indica que los datos se pasan a TCP, mientras que un valor igual a 17 indica que los datos se pasan a UDP.

El _número de protocolo_ especificado en el datagrama IP desempeña un papel análogo al del campo que almacena el _número de puerto_ en un segmento de la capa de transporte. El número de protocolo es el elemento que enlaza las capas de red y de transporte, mientras que el número de puerto es el componente que enlaza las capas de transporte y de aplicación.

## División en subredes

### 6. Para cada una de las siguientes direcciones IP (172.16.58.223/26, 163.10.5.49/27, 128.10.1.0/23, 10.1.0.0/24, 8.40.11.179/12) determine:

| Red              | Clase | Dir. subred | Max hosts | Dir broadcast | Rango |
| ---------------- | ----- | ----------- | --------- | ------------- | ----- |
| 172.16.58.223/26 | B     |             |           |               |       |
| 163.10.5.49/27   | B     |             |           |               |       |
| 128.10.1.0/23    | B     |             |           |               |       |
| 10.1.0.0/24      | A     |             |           |               |       |
| 8.40.11.179/12   | A     |             |           |               |       |
