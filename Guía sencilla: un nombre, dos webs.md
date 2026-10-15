# Práctica Apache - VirtualHost por nombre

## Objetivo: 

Configurar un servidor Apache en Ubuntu Server para utilizar el mismo nombre de dominio (www.smr.com) con dos puertos diferentes:
* Puerto 80: página de bienvenida.
* Puerto 9999: intranet protegida mediante usuario y contraseña.

## Paso 1 - Crear las carpetas ya las páginas

Se crearon las carpetas necesarias para las dos páginas: 

> sudo mkdir -p /var/www/smr/web /var/www/smr/intranet

Se creó la página de bienvenida: *echo "<h1>Bienvenidos a SMR</h1>" | sudo tee /var/www/smr/web/index.html*

Y la página de la intranet: *echo "<h1>Intranet de SMR</h1>" | sudo tee /var/www/smr/intranet/intranet.html*

## Paso 2 - Crear el usuario de la intranet

Se instaló apache2-utils: 

> sudo apt install apache2-utils -y

Después se creo el usuario alumno con contraseña: 

> sudo htpasswd -c /etc/apache2/.htpasswd alumno

El usuario alumno será utilizado posteriormente para acceder a la intranet.

## Paso 3 - Configurar el puerto 9999

Se modificó el archivo:

> sudo nano /etc/apache2/ports.conf

Se añadio:

> Listen 9999 debajo de Listen 80

De esta forma Apache queda preparado para escuchar tanto en el pueerto 80 como en el 9999.

Para guardar en nano: Ctrl+O, Enter y Ctrl+X para salir.

## Paso 4 - Crear el VirtualHost

Primero, abrimos el archivo de configuración:

> sudo nano /etc/apache2/sites-available/smr.conf

Dentro del archivo, escribimos la siguiente configuración:

<VirtualHost *:80>
    ServerName www.smr.com
    DocumentRoot /var/www/smr/web
</VirtualHost>

<VirtualHost *:9999>
    ServerName www.smr.com
    DocumentRoot /var/www/smr/intranet
    DirectoryIndex intranet.html

    <Directory /var/www/smr/intranet>
        AuthType Basic
        AuthName "Intranet SMR"
        AuthUserFile /etc/apache2/.htpasswd
        Require valid-user
    </Directory>
</VirtualHost>


Explicación de la configuración:

**VirtualHost:** permite configurar cada sitio web.

**ServerName:** indica el nombre de la web.

**DocumentRoot:** indica la carpeta donde están guardados los archivos de la página.

**DirectoryIndex:** indica que la página principal de la intranet es intranet.html.

**AuthType Basic:** activa la autenticación básica.

**AuthName:** indica el nombre de la zona protegida.

**AuthUserFile:** indica dónde se encuentra el archivo de usuarios y contraseñas.

**Require valid-user:** permite acceder únicamente a los usuarios con credenciales válidas.

Para guardar el archivo, pulsamos Ctrl + O, después Enter y finalmente Ctrl + X.

## Paso 5 - Activar el sitio y reiniciar Apache

En este paso vamos a activar nuestra configuración para que Apache pueda utilizarla.

Primero, habilitamos el sitio:

> sudo a2ensite smr.conf

Después, desactivamos el sitio predeterminado de Apache:

> sudo a2dissite 000-default.conf

A continuación, comprobamos que la configuración no tenga errores:

> sudo apachectl configtest

Si todo está correcto, aparecerá el mensaje:

> Syntax OK

Por último, reiniciamos Apache para aplicar los cambios:

> sudo systemctl restart apache2

Con estos pasos, Apache ya debería utilizar nuestra nueva configuración.

## Paso 6 - Comprobar que funciona

En este último paso vamos a comprobar que las dos páginas web funcionan correctamente.

### 6.1. Consultar la dirección IP del servidor

Ejecutamos el siguiente comando en la máquina virtual Ubuntu Server:

> ip a

Buscamos la dirección IP de la interfaz de red que utilizamos para conectarnos que es 192.168.56.10.

Debemos utilizar la dirección IP real de nuestra máquina virtual.

### 6.2. Comprobar las páginas desde el ordenador anfitrión

Abrimos el navegador del ordenador anfitrión y escribimos las siguientes direcciones, sustituyendo IP_DE_LA_VM por la IP real del servidor.

Primera página:

> http://192.168.56.10

Debe aparecer el mensaje:

> Bienvenidos a SMR

Segunda página:

> http://192.168.56.10:9999

Debe aparecer una ventana solicitando un usuario y una contraseña. Introducimos las credenciales creadas anteriormente.

Si los datos son correctos, debe aparecer el mensaje:

> Intranet de SMR

### 6.3. Acceder utilizando el nombre www.smr.com

Para acceder mediante el nombre de la web, utilizaremos una segunda máquina virtual que esté en la misma red que el servidor.

Primero, abrimos el archivo hosts de la segunda máquina virtual:

> sudo nano /etc/hosts

Añadimos una línea con la dirección IP real del servidor y el nombre de la web. Por ejemplo:

> 192.168.56.10 www.smr.com

Guardamos los cambios con Ctrl + O, pulsamos Enter y salimos con Ctrl + X.

Ahora abrimos el navegador de la segunda máquina virtual y probamos las dos direcciones:

> http://www.smr.com

Debe aparecer la página de bienvenida de SMR.

> http://www.smr.com:9999

Debe solicitar el usuario y la contraseña antes de mostrar la intranet.

Ambas páginas funcionan correctamente, terminé la práctica de configuración de VirtualHost por nombre con dos puertos y una intranet protegida con contraseña.











