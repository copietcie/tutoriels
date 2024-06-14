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

```
apt-get install apache2 php mariadb-server
mysql_secure_installation
```

![Securiser-MariaDB-pour-GLPI](https://github.com/kawaiiineko-website/tutoriels/assets/172619483/820eb6d2-db34-4bbd-a311-08d339849df7)

```
mysql -u root -p
```
```
create database zabbix character set utf8mb4 collate utf8mb4_bin;

create user zabbix@localhost identified by 'password';

grant all privileges on zabbix.* to zabbix@localhost;

set global log_bin_trust_function_creators = 1;

quit;
```

Puis prendre la suite du descriptif

## Etape 4
Paramétrage : joindre l'interface graphique en tapant <@IP>/zabbix sur un moteur de recherche

dans "collecte de données" > "hôtes" "créer un hôte" 

![image](https://github.com/kawaiiineko-website/tutoriels/assets/172619483/3b3093a6-6dbd-4b32-b89e-a8ab9b5678ff)

nom de l'hôte mettre le nom de la machine "Debian-12" si doute taper
```
lsb_release -a
```
 sur la machine cible
modele : cliquer sur selectionner puis selectionner "linux by zabbix agent"
groupe d'hôte : cliquer sur selectionner puis selectionner "linux servers"
pour l'interface cliquer sur ajouter > agent et mettre l'@IP de la machine à monitorer 

![image](https://github.com/kawaiiineko-website/tutoriels/assets/172619483/d3a15da9-fa91-468c-a8f2-3092df56a6e7)


dans "collecte de données" > "modèles" 

## Etape 5
Sur la machine à monitorer, l'agent est installé
aller dans 
```
cd /etc/zabbix/zabbix_agent2.conf
```
mettre l'@IP de la machine à la place de l'@IP localhost

![image](https://github.com/kawaiiineko-website/tutoriels/assets/172619483/b0cfe4ef-58f1-472f-95cf-3e51bd3384de)

mettre en commentaire l'@IP serveractive

![image](https://github.com/kawaiiineko-website/tutoriels/assets/172619483/bb702b6b-1ce5-4a27-92bb-41cb7a1c0ef3)

mettre le nom de la machine à la place de hostname

![image](https://github.com/kawaiiineko-website/tutoriels/assets/172619483/905b866e-b98c-4f0a-8d85-6062759108b9)

en root
```
systemctl restart zabbix-agent
```
