# Práctica: Instalación de MariaDB y PHP en Ubuntu 24.04
## 1. Objetivos
Los objetivos de esta práctica son:
* Comprender qué es una base de datos y por qué la necesita WordPress.
* Instalar MariaDB en Ubuntu 24.04 y comprobar su funcionamiento.
* Preparar el servidor para completar el entorno LAMP con PHP en los siguientes apartados.
* Documentar el proceso de instalación y las comprobaciones realizadas.
## 2. Apartado 1. Preparación del sistema
### 2.1. Actualización de la lista de paquetes
Comando ejecutado:
*sudo apt update*
Resultado obtenido:
La lista de paquetes se actualizó correctamente y el sistema volvió a mostrar el indicador de la terminal.
### 2.2. Comprobación del servicio Apache
Comando ejecutado:
*systemctl is-active apache2*
Resultado obtenido:
*Active*
Explicación:
El comando permite comprobar si el servicio Apache está funcionando. El resultado active indica que el servidor web está activo en ese momento.
Captura de pantalla:

## 3. Apartado 2. Instalación de MariaDB
### 3.1. Instalación del servidor
Comando ejecutado:
*sudo apt install mariadb-server -y*
Resultado obtenido:
La instalación finalizó correctamente y se pudo continuar utilizando la terminal.
### 3.2. Comprobación de la versión instalada
Comando ejecutado:
*mariadb --version*
Resultado obtenido:
*mariadb Ver 15.1 Distrib 10.11.14-MariaDB, for debian-linux-gnu (x86_64)*
Explicación:
Este comando muestra la versión de MariaDB instalada en el sistema. De esta forma, se comprueba que el programa está disponible desde la terminal.
Captura de pantalla:

### 3.3. Pregunta de reflexión
¿Qué diferencia hay entre mariadb-server y mariadb-client? ¿Cuál de los dos has instalado?
El paquete mariadb-server contiene el servidor que gestiona las bases de datos y atiende las peticiones. El paquete mariadb-client proporciona herramientas para conectarse al servidor y ejecutar consultas.
En esta práctica he instalado explícitamente mariadb-server. Durante la instalación también pueden instalarse herramientas cliente como dependencias.
## 4. Apartado 3. Comprobación del funcionamiento
## 4.1. Estado del servicio MariaDB
Comando ejecutado:
*sudo systemctl status mariadb*
Resultado obtenido:
*active (running)*
Explicación:
Este comando muestra el estado del servicio MariaDB. El estado active (running) indica que el servicio está funcionando actualmente.
### 4.2. Comprobación del inicio automático
Comando ejecutado:
*systemctl is-enabled mariadb*
Resultado obtenido:
*enabled*
Explicación:
Este comando comprueba si MariaDB está configurado para iniciarse automáticamente cuando arranca el sistema. El resultado enabled indica que el inicio automático está habilitado.
### 4.3. Acceso al monitor de MariaDB
Comando ejecutado:
*sudo mariadb*
Resultado obtenido:
*Welcome to the MariaDB monitor. Commands end with ; or \g.
Server version: 10.11.14-MariaDB-0ubuntu0.24.04.1 Ubuntu 24.04
MariaDB [(none)]>exit*
Explicación:
El comando permite entrar en el monitor de MariaDB utilizando permisos de administrador. Una vez dentro, el prompt cambia y permite introducir instrucciones SQL.
Capturas de pantalla:

### 4.4. Pregunta de reflexión
¿Qué diferencia hay entre active (running) y enabled? ¿Qué pasaría con WordPress si MariaDB estuviera activo pero no habilitado y se reiniciara el servidor?
Active (running) indica que el servicio está funcionando en ese momento, mientras que enabled indica que está configurado para arrancar automáticamente durante el inicio del sistema.
Si MariaDB estuviera activo pero no habilitado y se reiniciara el servidor, podría no iniciarse automáticamente.
En ese caso, WordPress podría mostrar errores al intentar acceder a la base de datos hasta que MariaDB volviera a iniciarse.

## 5.Apartado 4. Gestión del servicio MariaDB
### 5.1. Objetivo
En este apartado se comprueba que sabemos administrar el servicio MariaDB en Ubuntu 24.04 mediante systemctl. Este comando permite iniciar, detener, reiniciar y consultar el estado de los servicios del sistema.
### 5.2. Iniciar el servicio MariaDB
Para iniciar el servicio MariaDB, ejecutamos el siguiente comando:
*sudo systemctl start mariadb*
Este comando inicia el servicio de MariaDB si no se encuentra en ejecución.
A continuación, comprobamos su estado:
*sudo systemctl status mariadb*
El resultado muestra que el servicio se encuentra activo y funcionando (active (running)).
### 5.3. Reiniciar el servicio MariaDB
Para reiniciar MariaDB, ejecutamos:
*sudo systemctl restart mariadb*
Este comando detiene y vuelve a iniciar el servicio. Se utiliza, por ejemplo, para aplicar determinados cambios de configuración.
Después, comprobamos que continúa funcionando:
*systemctl is-active mariadb*
El resultado esperado es:
*active*
### 5.4. Habilitar el inicio automático
Para configurar MariaDB de forma que se inicie automáticamente cuando arranque el sistema, ejecutamos:
*sudo systemctl enable mariadb*
Este comando habilita el inicio automático del servicio durante el arranque de Ubuntu.
Es importante distinguir entre iniciar y habilitar un servicio: start lo pone en funcionamiento en ese momento, mientras que enable configura su inicio automático al arrancar el sistema.
Capturas de pantalla:


## 6. Detener MariaDB y comprobar la recuperación del servicio
### 6.1. Objetivo
En este apartado se comprueba qué ocurre cuando se detiene el servicio MariaDB y cómo podemos recuperar su funcionamiento. Esta prueba permite entender la importancia de mantener activo el servicio de bases de datos para que las aplicaciones web puedan conectarse a él.
### 6.2. Detener el servicio MariaDB
Para detener el servicio, ejecutamos:
*sudo systemctl stop mariadb*
A continuación, comprobamos su estado:
*systemctl is-active mariadb*
El resultado obtenido es:
*inactive*
Esto indica que MariaDB se encuentra detenido.
### 6.3. Comprobar la conexión con MariaDB
Con el servicio detenido, intentamos acceder al cliente de MariaDB mediante:
*sudo mariadb*
La conexión no se puede establecer porque el servidor MariaDB está detenido. El sistema muestra un mensaje de error de conexión.
Esta comprobación demuestra que, aunque el cliente esté instalado, necesitamos que el servicio del servidor esté funcionando para poder conectarnos a él.
### 6.4. Recuperar el servicio
Para recuperar el funcionamiento de MariaDB, ejecutamos:
*sudo systemctl start mariadb*
Después, volvemos a comprobar su estado:
*systemctl is-active mariadb*
El resultado obtenido es:
*active*
Esto confirma que el servicio se ha iniciado correctamente y vuelve a estar disponible.
### 6.5. ¿Cómo comprobaríamos un problema de conexión en WordPress?
Si WordPress no pudiera conectarse a su base de datos, comprobaríamos primero si MariaDB está funcionando:
*systemctl is-active mariadb*
Este comando permite conocer el estado del servicio. Si devuelve inactive, podemos intentar iniciarlo con:
*sudo systemctl start mariadb*
También podríamos probar una conexión local con:
*sudo mariadb*
Este segundo comando intenta acceder al servidor mediante el cliente de MariaDB usando privilegios de administrador.
Si el servicio está activo pero WordPress sigue sin conectarse, habría que revisar otros aspectos, como las credenciales de la base de datos, el nombre de la base de datos, la configuración de WordPress y los permisos del usuario.
Capturas de pantalla:

## 7. Instalación y configuración de PHP
### 7.1. Objetivo
El objetivo de este apartado es instalar PHP y los módulos necesarios para que Apache pueda ejecutar código PHP y para que las aplicaciones web puedan conectarse a MariaDB. PHP es un lenguaje de programación utilizado para desarrollar aplicaciones web dinámicas. Apache permite servir las páginas web y MariaDB almacena los datos de las aplicaciones.
### 7.2. Instalar PHP y los módulos necesarios
Ejecutamos el siguiente comando para instalar PHP, su integración con Apache y varios módulos adicionales:
*sudo apt install php libapache2-mod-php php-mysql php-curl php-gd php-mbstring php-xml php-zip php-intl -y*
### 7.3. Comprobar la versión de PHP
Una vez finalizada la instalación, comprobamos la versión instalada:
*php -v*
El sistema muestra información sobre la versión de PHP instalada. En esta práctica se ha instalado la rama PHP 8.3.
### 7.4. Reiniciar Apache
Para aplicar los cambios relacionados con la integración de PHP, reiniciamos Apache:
*sudo systemctl restart apache2*
A continuación, comprobamos que el servicio sigue funcionando:
*systemctl is-active apache2*
El resultado esperado es:
*active*
### 7.5. Comprobar los módulos de Apache
Ejecutamos el siguiente comando:
*sudo apache2ctl -M*
Este comando muestra los módulos cargados por Apache. Comprobamos que aparecen:
*mpm_prefork_module*
*php_module*
La presencia de estos módulos confirma que Apache está utilizando el módulo de PHP instalado para ejecutar código PHP.
### 7.6. Comprobar los módulos de conexión con MariaDB
Para comprobar los módulos de PHP relacionados con las bases de datos, ejecutamos:
*php -m | grep -Ei 'mysqli|mysqlnd|pdo_mysql'*
Este comando filtra la lista de módulos de PHP y muestra los que coinciden con mysqli, mysqlnd o pdo_mysql.
Estos módulos permiten a las aplicaciones PHP conectarse a bases de datos MySQL y MariaDB mediante distintas interfaces.
### 7.7. Comprobar que Apache ejecuta PHP
Para verificar que PHP se ejecuta desde Apache, creamos temporalmente un archivo de prueba:
*echo '<?php phpinfo();' | sudo tee /var/www/html/info.php*
Este comando crea el archivo info.php dentro del directorio web de Apache. La función phpinfo() muestra información detallada sobre PHP y su configuración.
Desde el navegador del ordenador, accedemos a la dirección:
*http://192.168.56.10/info.php*
Si la configuración es correcta, aparecerá una página con información de PHP.
### 7.8. Eliminar el archivo de prueba
Una vez realizada la comprobación, eliminamos el archivo:
*sudo rm /var/www/html/info.php*
Podemos comprobar que ya no está presente mediante:
ls /var/www/html
Es importante eliminar este archivo porque phpinfo() puede mostrar información sensible sobre la configuración del servidor, las versiones instaladas, los módulos y las rutas del sistema. No debe permanecer accesible en un servidor real.
### 7.9. ¿Por qué es necesario instalar php-mysql?
El paquete php-mysql proporciona los módulos que permiten a PHP comunicarse con servidores de bases de datos MySQL y MariaDB. Aplicaciones web como WordPress necesitan esta comunicación para consultar y guardar información, como usuarios, entradas, páginas y opciones de configuración. Sin los módulos adecuados de conexión a bases de datos, una aplicación PHP podría no ser capaz de acceder a la base de datos que necesita.
## 8. Comprobación final
### 8.1. Comprobar el estado de los servicios
Para finalizar la práctica, comprobamos que los servicios Apache y MariaDB se encuentran funcionando correctamente mediante el siguiente comando:
*systemctl is-active apache2 mariadb*
El resultado obtenido es:
> active
> active
Ambos servicios están activos, por lo que Apache puede atender las peticiones web y MariaDB está disponible para las aplicaciones que necesiten acceder a las bases de datos.
### 8.2. Resumen final de la arquitectura LAMP
Una vez realizadas las comprobaciones, podemos resumir los componentes instalados y su estado:

Pieza del LAMP

Programa

Estado

Linux

Ubuntu 24.04

Instalado

Apache

Apache2

Funcionando

MariaDB

MariaDB 10.11

Funcionando

PHP

PHP 8.3

Funcionando y preparado para MariaDB




































































