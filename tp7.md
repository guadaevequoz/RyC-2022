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
| Cantidad de hosts: 16777214 | Cantidad de hosts: 65534 | Cantidad de hosts: 254     |

### 4. ¿Qué son las subredes? ¿Por qué es importante siempre especificar la máscara de subred asociada?

Las subredes surgen cuando una red se vuelve muy grande. El concepto de máscara indica en una dirección IP qué bits son de red y qué bits son de host. Con el uso de redes con clases, la máscara estaba implícita en la dirección de clase, ya que se conocía a priori los bits para red y los bits para host. Cuando se creó el concepto de subredes también se les asoció una máscara de subred, que resultó de utilizar algunos bits de hosts para crear subredes y de esta manera obtener varias subredes con menos hosts cada una.

### 5. ¿Cuál es la finalidad del campo Protocol en la cabecera IP? ¿A qué campos de la capa de transporte se asemeja en su funcionalidad?

El campo _Protocol_ solo se suele emplear cuando un datagrama IP alcanza su destino final. El valor de este campo indica el protocolo específico de la capa de transporte al que se pasarán los datos contenidos en ese datagrama IP. Por ejemplo, un valor de 6 indica que los datos se pasan a TCP, mientras que un valor igual a 17 indica que los datos se pasan a UDP.

El _número de protocolo_ especificado en el datagrama IP desempeña un papel análogo al del campo que almacena el _número de puerto_ en un segmento de la capa de transporte. El número de protocolo es el elemento que enlaza las capas de red y de transporte, mientras que el número de puerto es el componente que enlaza las capas de transporte y de aplicación.

## División en subredes

### 6. Para cada una de las siguientes direcciones IP (172.16.58.223/26, 163.10.5.49/27, 128.10.1.0/23, 10.1.0.0/24, 8.40.11.179/12) determine:

| Red              | Clase | Dir. subred   | Max hosts | Dir broadcast | Rango |
| ---------------- | ----- | ------------- | --------- | ------------- | ----- |
| 172.16.58.223/26 | B     | 172.16.58.192 | 62        | 172.16.58.255 |       |
| 163.10.5.49/27   | B     | 163.10.5.32   | 30        | 163.10.5.     |       |
| 128.10.1.0/23    | B     | 128.10.0.0    | 510       |               |       |
| 10.1.0.0/24      | A     | 10.1.0.0      | 254       | 10.1.0.255    |       |
| 8.40.11.179/12   | A     | 8.32.0.0      | 1048574   |               |       |

### 7. Su organización cuenta con la dirección de red 128.50.10.0. Indique:

### a. ¿Es una dirección de red o de host?

**CONSULTAR**

### b. Clase a la que pertenece y máscara de clase.

Pertenece a la clase B. La máscara de esta clase es: `255.255.0.0`.

### c. Cantidad de hosts posibles.

`65634`

### d. Se necesitan crear, al menos, 513 subredes. Indique:

### i. Máscara necesaria.

`11111111 11111111 11111111 11000000`, lo que equivale a `255.255.255.192`

### ii. Cantidad de redes asignables.

2^10 = `1024`

### iii. Cantidad de hosts por subred.

2^6-2 = `62`

### iv. Dirección de la subred 710.

1. Le resto 1 a la subred y la escribo en binario: `1011000101`
2. Ubicar el número obtenido en la dirección IP ocupando la posición de los bits asignados a subred: `10000000 00110010 10110001 01000000` --> `128.50.177.64`

### 8. Si usted estuviese a cargo de la administración del bloque IP 195.200.45.0/24

**CONSULTAR**

### a. ¿Qué máscara utilizaría si necesita definir al menos 9 subredes?

### b. Indique la dirección de subred de las primeras 9 subredes.

### c. Seleccione una e indique dirección de broadcast y rango de direcciones asignables en esa subred.

### 9. Dado el siguiente gráfico:

<img src="img/tp7-ej9-enunciado.png">

### a. Verifique si es correcta la asignación de direcciones IP y, en caso de no serlo, modifique la misma para que lo sea.

### b. ¿Cuántos bits se tomaron para hacer subredes en la red 10.0.10.0/24? ¿Cuántas subredes se podrían generar?

### c. Para cada una de las redes utilizadas indique si son públicas o privadas.

## CIDR

### 10. ¿Qué es CIDR (Class Interdomain routing)? ¿Por qué resulta útil?

La estrategia de asignación de direcciones en Internet se conoce como _enrutamiento entre dominios sin clase_ (**CIDR, Classless Interdomain Routing**). CIDR generaliza la noción de direccionamiento de subred. Al igual que sucede con el direccionamiento de subredes, la dirección IP de 32 bits se divide en dos partes y de nuevo se expresa en notación decimal con puntos como a.b.c.d/x, donde x indica el número de bits de la primera parte de la dirección. Los x bits más significativos de una dirección en el formato a.b.c.d/x constituyen la parte de red de la dirección IP y a menudo se los denomina prefijo (o prefijo de red) de la dirección.

CIDR es útil ya que permite máscaras de subred de longitud variable (VLSM) para optimizar la asignación de direcciones IP y utilizar resumen de rutas para disminuir el tamaño de las tablas de enrutamiento.

### 11. ¿Cómo publicaría un router las siguientes redes si se aplica CIDR?

### a. 198.10.1.0/24

### b. 198.10.0.0/24

### c. 198.10.3.0/24

### d. 198.10.2.0/24

`198.10.0.0`. **CONSULTAR**

### 12. Listar las redes involucradas en los siguientes bloques CIDR:

- _200.56.168.0/21_:
- _195.24.0.0/13_:
- _195.24/13_:

**CONSULTAR**

### 13. El bloque CIDR 128.0.0.0/2 o 128/2, ¿Equivale a listar todas las direcciones de red de clase B? ¿Cuál sería el bloque CIDR que agrupa todas las redes de clase A?

Si, el bloque CIDR `128.0.0.0/2` equivale a todas las direcciones de red de la clase B.
El bloque CIDR `0.0.0.0/1` equivale a todas las redes de la clase A.

## VLSM

### 14. ¿Qué es y para qué se usa VLSM?

La técnica de VLSM (variable-length subnet masking) consiste en realizar divisiones en subredes con máscaras de longitud variable y es otra de las técnicas surgidas para frenar el agotamiento de direcciones IPv4. Básicamente, VLSM sugiere hacer varios niveles de división en redes para lograr máscaras más óptimas para cada una de las subredes que se necesiten.

## ICMP y Configuraciones IP
