Práctica Apache - VirtualHost por nombre
Objetivo: Configurar un servidor Apache en Ubuntu Server para utilizar el mismo nombre de dominio (www.smr.com) con dos puertos diferentes:
Puerto 80: página de bienvenida.
Puerto 9999: intranet protegida mediante usuario y contraseña.
Paso 1 - Crear las carpetas ya las páginas
Se crearon las carpetas necesarias para las dos páginas:
sudo mkdir -p /var/www/smr/web /var/www/smr/intranet
Se creó la página de bienvenida:
echo "<h1>Bienvenidos a SMR</h1>" | sudo tee /var/www/smr/web/index.html
Y la página de la intranet:
echo "<h1>Intranet de SMR</h1>" | sudo tee /var/www/smr/intranet/intranet.html
