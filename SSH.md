# Gestionando un servidor por SSH

## 1. ¿Qué es SSH?

SSH (Secure Shell) es un protocolo de red que permite conectarse de forma remota y segura a otro equipo a través de una conexión cifrada. Se utiliza para administrar servidores mediante una terminal, ejecutar comandos y gestionar su configuración sin necesidad de acceder físicamente a ellos.

Por defecto, SSH utiliza el puerto 22/TCP.

## 2. Configuración SSH

Para administrar un servidor mediante SSH, es necesario disponer de un servidor SSH instalado y configurado en el equipo remoto, así como de un cliente SSH desde el equipo desde el que se realizará la conexión.

En sistemas Linux, como Ubuntu, se puede utilizar el servicio OpenSSH Server para permitir conexiones remotas.

### 2.1. Configuración de las interfaces de red

Antes de establecer una conexión SSH, es importante conocer las interfaces de red del servidor y comprobar qué dirección IP tiene asignada cada una. Una interfaz de red es el componente que permite a un equipo conectarse a una red. Puede ser física, como una tarjeta Ethernet, o virtual, como las interfaces que crean los programas de virtualización.

Para consultar las interfaces de red y sus direcciones IP en Linux, se utiliza el siguiente comando:
> ip addr

Este comando muestra las interfaces disponibles, su estado y las direcciones IP asignadas.

Las interfaces más habituales son:

*lo:* interfaz de loopback o bucle local. Permite que el equipo se comunique consigo mismo. Normalmente utiliza la dirección 127.0.0.1 en IPv4.

*enp0s3, ens33 o similares:* interfaces Ethernet que permiten la conexión a una red. El nombre depende del sistema y del entorno de virtualización.


En una máquina virtual pueden aparecer varias interfaces de red según la configuración utilizada. Por ejemplo:


*NAT:* permite que la máquina virtual acceda a otras redes a través del equipo anfitrión. Para conectarse desde el anfitrión al servidor, puede ser necesario configurar el reenvío de puertos.


*Adaptador puente:* conecta la máquina virtual a la misma red local que el equipo anfitrión, de modo que puede obtener una dirección IP de esa red y ser accesible desde otros dispositivos, según las reglas de red y el cortafuegos.


*Red interna o solo-anfitrión:* permite la comunicación entre determinados equipos virtuales o entre la máquina virtual y el anfitrión, según el modo elegido, sin proporcionar necesariamente acceso a Internet.

Para conectarse por SSH, hay que identificar la interfaz adecuada y la dirección IP que permite alcanzar el servidor desde el equipo cliente.

### 2.2. Comprobación de la conexión

Una vez identificada la dirección IP del servidor, se puede comprobar la conectividad desde el equipo cliente utilizando: *ping 192.168.56.10* (Dirrección IP del Servidor)

Este comando permite comprobar si el servidor responde a las solicitudes ICMP, siempre que la red y el cortafuegos lo permitan.

Posteriormente, si el servicio SSH está instalado y activo, se puede establecer una conexión con el siguiente comando: *ssh saherimtiaz@192.168.56.10*

Se debe sustituir usuario por el nombre de usuario del servidor y Dirrección IP del Servidor por la dirección IP correspondiente.

Al conectarse por primera vez, SSH puede solicitar que se verifique la identidad del servidor. Después de confirmar la clave del servidor, se solicitarán las credenciales o se utilizará el método de autenticación configurado.

De esta forma, se puede administrar el servidor remotamente mediante una conexión cifrada.










