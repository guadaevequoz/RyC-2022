## Práctica 2 - Capa de Aplicación - DNS

## DNS

### 1. Investigue y describa cómo funciona el DNS. ¿Cuál es su objetivo?

DNS sirve para traducir los nombres de host a su direccion IP correspondiente, esto sirve para que cuando queramos comunicarnos con otras terminales no tengamos que buscarlo por su nombre IP, sino simplemente escribimos su mnemónico. DNS es: una base de datos que contiene las IPs de los nombres de host, y también es un protocolo de la capa de aplicación que permite a los hosts consulta su BD. Se ejecuta sobre UDP y utiliza el puerto 53.

### 2. ¿Qué es un root server? ¿Qué es un generic top-level domain (gtld)?

Un root server es aquel que proporciona las direcciones IP de los servidores TLD. <br>
Un gTLD es una de las categorias de TLD, la cual alberga extensiones globales para los nombres de dominio, suelen aparecer al final de los mismos. Algunos ejemplos son: (.com, .net, .org).

### 3. ¿Qué es una respuesta del tipo autoritativa?

Una respuesta autoritativa sucede cuando una consulta DNS es respondida por el servidor autoritativo que alberga un nombre de dominio. Si la respuesta es emitida por un DNS local, sin este ser parte del servidor autoritativa, entonces es no-autoritativa.

### 4. ¿Qué diferencia una consulta DNS recursiva de una iterativa?

Una consulta recursiva es aquella que envia a un mismo servidor una consulta hasta que la respuesta sea, en efecto, la dirección IP del host que consulto (cuando la obtiene no consulta más). Una consulta recursiva es aquella que puede consultar con varios servidores DNS y recibir respuestas que, quizás, no tengan la dirección IP que requeria, sino que un camino para llegar a ella a traves de los servidores DNS de ella.

### 5. ¿Qué es el resolver?

Un resolver es una parte del sistema operativo que se encarga de realizar las consultas a un servidor DNS, interpretarlas y devolverlas al programa que ha efectuado la consulta. Los servidores DNS también pueden incorporar un resolver, que gestiona las consultas que un servidor DNS debe hacer.
Un resolver suele hacer sólo consultas recursivas.

### 6. Describa para qué se utilizan los siguientes tipos de registros de DNS:

- **A:** Proporciona la respuesta estándar nombre de host-dirección IP. El valor `nombre` es un nombre de un host y `valor` es la dirección IP que le corresponde a dicho nombre. Por ejemplo: (relay.bar.foo.com,145.37.93.126,A) es un registro A.

- **MX:** Permiten a los nombres de host de los servidores de correo tener alias simples. Utilizando este registro, las empresas pueden tener el mismo alias para su servidor de correo que para otros servidores. El `nombre` es un alias y `valor`es el nombre canonico del servidr. Por ejemplo (foo.com, mail.bar.foo.com, MX) es un registro MX.

- **PTR:** Este registro este hace referencia a un punto de terminación de red. Es decir, que la sintaxis de DNS es la responsable del mapeo de una dirección IPv4 para el CNAME en el alojamiento. En otras palabras, es lo contario al registro A ya que A apunta a una IP y PTR resuelve una IP a un nombre de dominio.

- **AAAA:** Es igual a A con la diferencia que contiene la dirección IPv6 de un dominio, en vez de IPv4 que es la version que utiliza A. En este caso, las direcciones IPv6 necesitan de 128 bits, por lo cual el valor rdlenght también será fijo. Por este motivo se denomina AAAA, siendo cuatro veces más larga que A.

- **SRV:** Este registro hace referencia a "Servicio". Se utiliza para la definición de un servicio TCP en el que opera el dominio.

- **NS:** Este registro se utiliza para enrutar las consultas DNS a lo largo de las cadenas de consulta. El `nombre` es un dominio y el `valor` es el nombre de host de un servidor DNS autoritativo que sabe cómo obtener las direcciones IP de los host de dominio. Por ejemplo: (foo.com, dns.foo.com, NS) es un registro NS.

- **CNAME:** Este registro puede proporcionar a los host que hacen consultas el nombre canónico correspondiente a un nombre de host. El `valor` es un nombre de host canónico correspondiente al alias especificado por `nombre`. Por ejemplo: (foo.com, relay1.bar.foo.com) es CNAME.

- **SOA:** Este registro hace referencia al comienzo de autoridad. Este registro es uno de los registros DNS más importantes porque guarda información esencial como la fecha de la última actualización del dominio, otros cambios y actividades. En este tipo de transferencias se copian archivos en otros servidores con la finalidad de evitar fallos. Esto también controla la propagación del archivo original.

- **TXT:** Este registro hace referencia a un texto. Permite que el administrador inserte texto en la consulta DNS. Esto se utiliza para dejar notas sobre la información de dominio.

### 7. En Internet, un dominio suele tener más de un servidor DNS. ¿Por qué cree que esto es así?
