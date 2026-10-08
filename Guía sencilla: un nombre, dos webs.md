# Práctica Apache - VirtualHost por nombre
## Objetivo: Configurar un servidor Apache en Ubuntu Server para utilizar el mismo nombre de dominio (www.smr.com) con dos puertos diferentes:
* Puerto 80: página de bienvenida.
* Puerto 9999: intranet protegida mediante usuario y contraseña.
### Paso 1 - Crear las carpetas ya las páginas
Se crearon las carpetas necesarias para las dos páginas:
sudo mkdir -p /var/www/smr/web /var/www/smr/intranet
Se creó la página de bienvenida:
echo "<h1>Bienvenidos a SMR</h1>" | sudo tee /var/www/smr/web/index.html
Y la página de la intranet:
echo "<h1>Intranet de SMR</h1>" | sudo tee /var/www/smr/intranet/intranet.html 
### Paso 2 - Crear el usuario de la intranet
Se instaló apache2-utils:
sudo apt install apache2-utils -y
Después se creo el usuario alumno con contraseña: 
sudo htpasswd -c /etc/apache2/.htpasswd alumno
El usuario alumno será utilizado posteriormente para acceder a la intranet.
### Paso 3 - Configurar el puerto 9999
Se modificó el archivo:
sudo nano /etc/apache2/ports.conf
Se añadio:
Listen 9999 debajo de Listen 80
De esta forma Apache queda preparado para escuchar tanto en el pueerto 80 como en el 9999

