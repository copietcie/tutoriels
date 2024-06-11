# Installation GLPI
Tutoriel pour installer GLPI et mettre en place une authentification LDAP

## Etape 1
Depuis la VM, télécharger l'archive après avoir récupérer le lien pointant sur le bouton : https://glpi-project.org/downloads/
```
cd /tmp
wget https://github.com/glpi-project/glpi/releases/download/10.0.15/glpi-10.0.15.tgz
tar xzvf glpi-X.Y.Z.tgz
mv glpi /var/www/html/glpi
chown -R www-data:www-data /var/www/html
```
Changement des chemins de certains répertoires glpi pour une meilleure sécu : 
```
mv /var/www/html/glpi/config /etc/glpi/ && chown -R www-data:www-data /etc/glpi
mv /var/www/html/glpi/files /var/lib/glpi/ && chown -R www-data:www-data /etc/glpi
mkdir -p /var/log/glpi/ && chown -R www-data:www-data /var/log/glpi/
```
Indiquer que les conf de GLPI est dans /etc/glpi : 
```
nano /var/www/html/glpi/inc/downstream.php
```
```
<?php
define('GLPI_CONFIG_DIR', '/etc/glpi/');

if (file_exists(GLPI_CONFIG_DIR . '/local_define.php')) {
   require_once GLPI_CONFIG_DIR . '/local_define.php';
}
```
Indiquer où se trouve le répertoire de log et de lib :
```
nano /etc/glpi/local_define.php
```
```
<?php
define('GLPI_VAR_DIR', '/var/lib/glpi');
define('GLPI_LOG_DIR', '/var/log/glpi');
```

## Etape 2 
Installation du serveur LAMP + PHP pré-requis: 
```
 apt-get install -y apache2 mariadb-server php
 mysql_secure_installation
 apt-get install -y php-mysqli php-dom php-simplexml php-xmlreader php-xmlwriter php-curl php-gd php-intl php-ldap php-bz2 php-zip php-mbstring
```
## Etape 3
Configuration php : 
```
 nano /etc/php/8.2/apache2/php.ini
```
changer la variable session.cookie_httponly à "on"
```
 session.cookie_httponly = on
```
Configuration Vhost : 
```
 cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/glpi.conf
 a2dissite 000-default.conf
 a2ensite glpi.conf
 apachectl -t
 systemctl reload apache2
```
Vhost complet sécurisé (pour le 80): 
```
<VirtualHost *:80>
        ServerName glpi.interne.fr
        DocumentRoot /var/www/html/glpi/public
        <Directory /var/www/html/glpi/public>
                Require all granted
                RewriteEngine On
                RewriteCond %{REQUEST_FILENAME} !-f
                RewriteRule ^(.*)$ index.php [QSA,L]
        </Directory>
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
Configuration BDD : 
```
 mysql -u root -p
 create database glpi_db;
 create user 'glpi_db_user'@'%' identified by 'the_password123!';
 grant all privileges on glpi_db.* to 'glpi_db_user'@'%';
```
## Etape 4
Ajout SSL + forcer le SSL
```
mkdir /etc/apache2/certs
openssl req -new -newkey rsa:2048 -days 365 -nodes -x509 -keyout glpi.key -out glpi.crt
chown -R www-data:www-data /etc/apache2/certs
```

Activer le module apache de SSL puis créer un vhost ssl ou éditer celui existant pour écouter sur le port 443 : 

```
a2enmod ssl
```
```
<VirtualHost *:443>
        SSLEngine on
        SSLCertificateFile      /etc/apache2/certs/glpi.crt
        SSLCertificateKeyFile   /etc/apache2/certs/glpi.key
</VirtualHost>
```
```
systemctl restart apache2
```


![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/c85e340b-0e04-476a-8eeb-940747809e71)

## Etape 5
Activer l'authentification LDAP 

* Configuration > Authentification > Annuaire LDAP > + Ajouter
* Ajouter un compte en Read Only sur l'AD pour GLPI
* ![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/cd58c195-e938-480e-b210-1868d81f6adc)

* Connecter le serveur GLPI et le LDAP avec ce filtre :
```
(&(objectClass=user)(objectCategory=person)(!(userAccountControl:1.2.840.113556.1.4.803:=2)))
```
Si ça ne sort rien, c'est que ça peut être un problème sur le filtre ou le champ de l'identifiant (uid peut être en non défini) alors passer à userprincipalname dans le champ "Champ de l'identifiant".




