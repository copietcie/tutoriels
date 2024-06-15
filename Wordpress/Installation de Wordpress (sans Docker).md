# Installation de Wordpress

## Etape 1
Après avoir installé une machine sur Debian et LAMP, récupérer l'archive de Wordpress sur ce lien : https://fr.wordpress.org/download/
```
cd /tmp
wget https://fr.wordpress.org/latest-fr_FR.zip
apt-get update && apt-get install -y unzip
unzip latest-fr_FR.zip
```
=> Adapter le nom de l'archive si différent

Déplacer dans l'endroit souhaité et adapter les droits : 
```
mv wordpress/ /var/www/html/wordpress
chown -R www-data:www-data /var/www/html/wordpress/
chmod -R 755 /var/www/html/wordpress/
```

## Etape 2
Faire un VHOST : 
```
cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/wordpress.conf
```

Exemple du contenu : 

<VirtualHost *:80>
        ServerName wordpress.myenterprise.com
        ServerAlias www.wordpress.myenterprise.com
        DocumentRoot /var/www/html/wordpress
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

## Etape 3 
Faire une base de données pour Wordpress : 
```
create database wordpress_db;
create user 'wordpress_user'@'%' IDENTIFIED BY 'password';
grant all privileges on wordpress_db.* to 'wordpress_user'@'%';
flush privileges;
quit;
```

## Etape 4
Lancer un navigateur et se connecter sur le serveur web : http://IP_DU_SERVER_WORDPRESS pour faire l'installation : 

![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/136aa9f5-da10-4d9e-984c-76dcda3dec33)

* Configurer la connexion à la BDD :
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/6a670e01-6489-4a2c-bef4-d86583f247ec)

* **Nom de la base de données** : Le nom de la base de données dédié à Wordpress créé au dessus
* **Identifiant** : Le compte crée au dessus avec les droits sur la BDD pour Wordpress
* **Mot de passe** : Le mot de passe du compte crée au dessus avec les droits sur la BDD pour Wordpress
* **Adresse de la base de données** : La machine qui héberge la base de données (IP)

![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/82a50aa9-32a7-4526-ab25-c393912a6b02)

* Saisir le titre du site et choisir les credentials pour un compte Admin
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/036050af-e897-4998-836b-000b52d4c8f7)

Tenter ensuite la connexion : 
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/95a9c681-cc25-4359-9b31-cf8916f42976)

Wordpress est installé, suite intéressante : 
* Certificat SSL : https://github.com/kawaiiineko-website/tutoriels/tree/main/Certificat%20SSL
* Bloquer le répertoire /wp-admin : https://github.com/kawaiiineko-website/tutoriels/blob/main/Wordpress/wpadmin.md
* Ajouter le module e-commerce : https://github.com/kawaiiineko-website/tutoriels/blob/main/Wordpress/Ecommerce.md
