# basic-serve-setup
Basic server setup PHP, Mysql and Apache in Ubuntu Server

---------------

sudo apt-get update

##Apache
sudo apt-get install apache2

##activar rewrite de apache
sudo a2enmod rewrite

##reiniciar apache
sudo service apache2 restart

##Mysql
sudo apt-get install mysql-server
sudo mysql_secure_installation

##parar y arrancar mysql
sudo /etc/init.d/mysql stop
sudo /etc/init.d/mysql start

##entrar a mysql 
mysql -u root -p

##cambiar contrase de usuario
SET PASSWORD FOR 'root'@'localhost' = PASSWORD('MyNewPass');

##crear bd
create database nombre;

##crear usuario (para acceso remoto se debe crear localhost y %)
CREATE USER 'nombre_usuario'@'localhost' IDENTIFIED BY 'tu_contrasena';
GRANT ALL PRIVILEGES ON * . * TO 'nombre_usuario'@'localhost';
FLUSH PRIVILEGES;

##acceso remoto
modificar my.cnf (/etc/mysql/) y agregar bind-address bajo la etiqueta [mysqld]
bind-address = 0.0.0.0  (cualquier ip)
o una IP específica

##php
apt-get -y install php7.0 libapache2-mod-php7.0
apt-get install php7.0-mysql php7.0-cli php7.0-gd php7.0-json php7.0-mbstring php-xml
apt-get install php7.0-zip  php7.0-gd

##composer
curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer

##git
sudo apt-get install git


##Urls amigables
editar el archivo /etc/apache/sites-enabled/000-default.conf y agregar
<Directory /var/www/html>
                Options Indexes FollowSymLinks MultiViews
                AllowOverride All
                Order allow,deny
                allow from all
</Directory>

para asignar dominios y subdominos ver
1. Se debe crear una replica de apache2/sites-available/00-algo.conf
con el nombre del sitio
2. Se edita esta nuevo archivo indicando la ruta del sitio y el dominio o subdominio que se va a usar
3. Se agrega el directory
<Directory /var/www/html/yoursite.com/laravelappinstall/public/>
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
</Directory>
Ver solucion final en http://laravel.io/forum/09-15-2015-removing-indexphp-from-url-laravel-5116


##Permisos deploy laravel
En proyectos laravel se debe dar permiso de escritura a los directorios bootstrap/cache y storage

