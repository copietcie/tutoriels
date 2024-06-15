# Installation de Nextcloud

## Etape 1
* Installer une Debian puis installer Apache2, MariaDB et PHP (LAMP)
```
apt-get update && apt-get install -y apache2 mariadb-server php
```

* Mettre les modules PHP nécessaires : 
```
apt-get update && apt-get install -y php-ldap php-zip php-dom php-xml php-mbstring php-gd php-simplexml php-curl php-mysql
```

## Etape 2
* Aller sur le site https://nextcloud.com/install/#instructions-server et descendre jusqu'à la partie "Community Project" puis "Archive" et récupérer la .tar.bz2 (Faire clic droit pour copier le lien)
Sur la Debian, récupérer l'archive
```
cd /tmp
wget https://download.nextcloud.com/server/releases/latest.tar.bz2
```
=> Où le lien est celui que nous avons copié au dessus.

* Extraire l'archive : 
```
tar -vfx latest.tar.bz2
```
=> Si le nom de l'archive est différente, adapter.

* Déplacer l'archive décompressée de Nextcloud dans l'endroit voulu ou dans le répertoire principal d'Apache et adapter les droits
```
mv nextcloud/ /var/www/html/nextcloud
chown -R www-data:www-data /var/www/html/nextcloud/
chmod -R 755 /var/www/html/nextcloud/
```

## Etape 3

* Copier le fichier template du VHOST par défaut et le nommer : 
```
cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/nextcloud.conf
```

* Voici une configuration basique : 
```
<VirtualHost *:80>
        ServerName nextcloud.myenterprise.com
        ServerAlias www.nextcloud.myenterprise.com
        DocumentRoot /var/www/html/nextcloud
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
        <Directory /var/www/htmlnextcloud/>
                Require all granted
                AllowOverride All
                Options FollowSymLinks MultiViews
                <IfModule mod_dav.c>
                        Dav off
                </IfModule>
        </Directory>
</VirtualHost>
```

Désactiver le VHOST par défaut d'Apache et activer le VHOST pour Nextcloud : 
```
a2endissite 000-default.conf
a2ensite nextcloud.conf
```

Check de la conf avant redémarrage
```
apachectl -t
```
Activer les modules apache : 
```
a2enmod headers
a2enmod env
a2enmod dir
a2enmod mime
a2enmod ssl
```
=> Certains modules peuvent déjà être activé par défaut.

Relancer Apache : 
```
systemctl restart apache2
```

## Etape 4
Création de la base de données pour Nextcloud 

* Installation sécurisé :
```
mysql_secure_installation
```

* Création de la base :
```
create database nextcloud_db;
```

* Création de l'utilisateur et son mot de passe
```
create user 'nextcloud_user'@'%' IDENTIFIED BY 'password'; 
```

* Donner tous les droits sur la base à l'utilisateur créé :
```
grant all privileges on nextcloud_db.* to 'nextcloud_user'@'%';
```

* RElancer les tables/droits :
```
flush privileges;
quit;
```

## Etape 5
Configuration finale et installation via le navigateur

* Lancer un navigateur et se rendre sur http://ip_du_server_nextcloud

On arrive sur la page d'installation où il faut indiquer des valeurs : 
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/b87ae29d-a47c-4978-9b72-a76373ac148d)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/a2a88aa4-31aa-4aa1-90e1-0fe01469570f)

* **S’identifier** : Nom du nouvel utilisateur (Administrateur)
* **Mot de passe** : Mot de passe du nouvel utilisateur (Administrateur)
* **Répertoire des données** : L'endroit où seront stockés les données envoyés sur le cloud (laissez par défaut)
* **Compte de base de données** : Le compte crée au dessus avec les droits sur la BDD pour Nextcloud
* **Mot de passe de la base de données**: Le mot de passe du compte crée au dessus avec les droits sur la BDD pour Nextcloud
* **Nom de la base de données** : Le nom de la base de données dédié à Nextcloud créé au dessus
* **Hôte de la base de données** : La machine qui héberge la base de données (IP) et le port à indiquer (par défaut : 3306)

* Cliquer sur **Installer** et attendre.
* Les applications recommandées ne sont pas spécialement nécessaires et sont installables ultérieurement, les installer maintenant peut allonger le temps
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/24188b5b-fe31-4f8b-b120-ebcb65e818f6)


