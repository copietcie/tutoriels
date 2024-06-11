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
Configuration BDD : 
```
 mysql -u root -p
 create database glpi_db;
 create user 'glpi_db_user'@'%' identified by 'the_password123!';
 grant all privileges on glpi_db.* to 'glpi_db_user'@'%';
```





Pourquoi externe et autoriser le partage ? => Cela permettra à la VM de se connecter sur le réseau externe et de récupérer un bail du serveur DHCP (mode bridge) => Cocher l'autorisation permet de partager la carte réseau aux VM
Pourquoi interne ? => Cela permet de faire un réseau "interne" entre VM et l'hyperviseur (grâce à une carte réseau sur l'hyperviseur)
Pourquoi privé ? => Cela permet de faire un réseau "isolé" entre plusieurs VM mais l'hyperviseur ne peut plus communiquer avec (sauf s'il y a un PFSENSE)


## Création des VM
* Créer les VM qui vont faire tourner Pfsense puis leur ajouter les 3 cartes réseaux qu'on vient de créer ci-dessus (Paramètres > Ajouter un matériel > Carte réseau > Le nom de la carte réseau)
* ![image](https://github.com/kawaiiineko-website/pfsense-carp/assets/118014015/51d057ae-9bf6-4c48-bb18-6f541d3d78e5)
* ![image](https://github.com/kawaiiineko-website/pfsense-carp/assets/118014015/7679b27f-ba8e-4c7c-8e87-ab28ddbf123e)
* Penser à activer l'usurpation de la MAC adress sur toutes les interfaces réseaux
* ![image](https://github.com/kawaiiineko-website/pfsense-carp/assets/118014015/74da61e3-183b-43ce-b6c0-6bde9c2f8b06)



## Lancement de la VM
* Une fois l'OS installé, assigner les interfaces dans le bon ordre et configurer les interfaces réseaux (WAN en DHCP, LAN en static avec un serveur DHCP et OPT1/PFSYNC en static en réseau /29)

## Configuration interfaces via l'interface web
* Décocher ces deux cases sur l'interface WAN : ![image](https://github.com/kawaiiineko-website/pfsense-carp/assets/118014015/6963902a-9c79-46cb-b952-1369675f93aa)
* Renommer l'interface OPT1 en PFSYNC : ![image](https://github.com/kawaiiineko-website/pfsense-carp/assets/118014015/e63b8347-74ea-42f9-a399-a1dbb3efa8a5)

## Configuration HA & VIP
* System > High Availability > Cocher "pfsync transfers state insertion, update, and deletion messages between firewalls"
* Choisir l'interface PFSYNC
* Mettre l'IP de l'autre PFSence sur "pfsync Synchronize Peer IP"
* Sur le MASTER seulement :
  * Synchronize Config to IP : mettre l'IP du PFSense esclave
  * Remote System Username : utilisateur admin
  * Remote System Password : son mdp
  * Synchronize admin : à cocher si besoin de synch les comptes
  * Select options to sync : choisir les options à dupliquer sur le second PFSense
  * ![image](https://github.com/kawaiiineko-website/pfsense-carp/assets/118014015/77ae0e4d-b110-45d5-aa8f-050147060c0b)
  * ![image](https://github.com/kawaiiineko-website/pfsense-carp/assets/118014015/0c5fa2a9-3906-4cdd-9941-ae088552f988)
  * Aller dans Firewall > Virtual IPs > Add > Sélectionner "Carp" > Mettre l'IP virtuelle dans "Adresses" avec le bon masque > Mettre un mot de passe dans Virtual IP Password > Mettre un ID de groupe dans VHID Group > Mettre le Skew à 0 pour que ça soit considéré comme le master dans Advertising frequency
  * ![image](https://github.com/kawaiiineko-website/pfsense-carp/assets/118014015/75dd1d3e-585e-4d63-b287-08a7254c25f1)
 
* Sur le MASTER et le SLAVE, autoriser les flux sur l'interface PFSYNC (any/any) ou filtrer (inutile)
* Tester le ping entre les deux parefeu sur l'interface PFSYNC

## Regarder le STATUS 

* Aller dans Status > CARP (failover) et checker qu'il y a bien un MASTER et un BACKUP.
* ![image](https://github.com/kawaiiineko-website/pfsense-carp/assets/118014015/8ff352df-3f08-4e59-8cdd-a55251838978)
* ![image](https://github.com/kawaiiineko-website/pfsense-carp/assets/118014015/29b4778e-1f02-4ec0-a91e-2f9c09930e0c)

## Configurer le serveur DHCP (en LAN)
* Mettre la gateway sur l'IP virtuelle LAN

## Tester
* Lancer un ping en continu depuis une machine sur le réseau sur le(s) IP virtuelle et regarder si la bascule se fait et en combien de temps : 
* ![image](https://github.com/kawaiiineko-website/pfsense-carp/assets/118014015/fac0df7e-a19d-4989-bad1-c9e45ad4acb4)

* Commande PING en continu sur Windows
```
ping X.Y.Z.A /t
```
