# Installation de Zabbix

## Etape 1
Installation d'une machine Debian standard

## Etape 2
Aller sur le site https://www.zabbix.com/fr/download
Choisir la plateforme selon notre machine et si l'on veut installer le server 

![image](https://github.com/kawaiiineko-website/tutoriels/assets/172619483/b3077f72-b531-4fa3-975f-4eab36c1b047)

ou un agent

![image](https://github.com/kawaiiineko-website/tutoriels/assets/172619483/77217c93-f9b1-4ba5-8d4d-c838704a7905)

## Etape 3
Suivre les indications qui suivent pour l'installation

A l'étape C-
Installer une base de donnée en installant mariadb-server et en parametrant la BDD

apt-get install apache2 php mariadb-server
mysql_secure_installation

![Securiser-MariaDB-pour-GLPI](https://github.com/kawaiiineko-website/tutoriels/assets/172619483/820eb6d2-db34-4bbd-a311-08d339849df7)

mysql -u root -p
create database zabbix character set utf8mb4 collate utf8mb4_bin;
create user zabbix@localhost identified by 'password';
grant all privileges on zabbix.* to zabbix@localhost;
set global log_bin_trust_function_creators = 1;
quit;

Puis prendre la suite du descriptif

## Etape 4
Paramétrage
