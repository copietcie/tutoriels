# Installation de Portainer avec Docker Compose
* Script d'installation de Docker
```
#!/bin/bash
# Add Docker's official GPG key:
  apt-get update
  apt-get install ca-certificates curl -y
  install -m 0755 -d /etc/apt/keyrings
  curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
  chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/deb>  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
    tee /etc/apt/sources.list.d/docker.list > /dev/null
  apt-get update
# Install all the packages of Docker
apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-compose -y
```
Vérifier que Docker est bien installé en lançant un container Hello world:
```
docker run hello-world
```
Ce message = On peut passer à la suite : 
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/6a49fb4f-1970-49bb-8236-4a78c57c1891)

* Fichier d'installation de Portainer (en stack avec Docker Compose)
```
services:
  portainer:
    image: portainer/portainer-ce:latest
    ports:
      - 8000:8000
      - 9443:9443
    restart: always
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - portainer_data:/data
volumes:
  portainer_data:
```
Pour check la conf du compose : 
```
docker compose -f <name_of_the_yml_file.yml> config
```
Pour le lancer : 
```
docker compose -f <name_of_the_yml_file.yml> up -d
```
Se rendre ensuite sur Portainer Web UI (https://IP_DE_LA_VM_DOCKER:9443) => Pas l'ip du conteneur la VM la COQUE
* La première fois, il faut choisir le nom d'utilisateur et le mot de passe du compte administrateur de Portainer
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/106682a8-8e7e-49c7-8e42-b35bf740af4c)



Fichier d'installation de Nginx Proxy Manager (en stack avec Docker Compose)
```
services:
  nginx_proxy_manager:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '80:80'
      - '81:81'
      - '443:443'
    volumes:
      - nginx_data:/data
      - nginx_ssl:/etc/letsencrypt
volumes:
  nginx_data:
  nginx_ssl:
```
Se rendre ensuite sur Nginx Proxy Manager en mode web (http://IP_DE_LA_VM_DOCKER:81) => Pas l'ip du conteneur la VM la COQUE
* Mail par défaut : admin@example.com
* Mot de passe par défaut : changeme

On est directement amener à changer le mail et le mot de passe.

Il n'aura que quelques confs comme la redirection vers les conteneurs en fonction du nom de domaine et l'ajout du SSL : 
* Redirection :
  *  Faire Hosts > Proxy Hosts
  ![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/7629f60a-80c2-40d0-80b9-e6215445850f)
  *  Faire Add Proxy
    * **Domain Names** : Choisir le nom de domaine pour le conteneur désiré
    * **Scheme** : Choisir si c'est http ou https
    * **Forward Hostname / IP** : Choisir l'IP du conteneur, ou son IP Gateway ou le nom du conteneur
    * **Forward Ports** : Choisir le port du HTTP ou HTTPS sur lequel le conteneur écoute
    * Activer le **Websocket Support**
    * Mettre **Publicy Accessible**
* SSL
  * Générer au préalable un certificat SSL avec sa clé (faire un wildcard pour protéger tous les sous domaine d'un seul domaine, ça évitera d'avoir 600 certificats par domaine)
  * Se mettre dans une machine Linux et lancer cette commande pour générer une paire de certificat et de clé
  * ``` openssl req -new -x509 -days 365 -nodes -out _.myenterprise.com.crt -keyout _.myenterprise.com.key ```
  * Afficher chaque fichier (_.myenterprise.com.crt && _.myenterprise.com.key) puis faire un fichier sur le Windows avec le même nom et le même contenu (```cat _.myenterprise.com.crt``` & ```cat _.myenterprise.com.key```) sinon faire du scp
  * Aller dans **SSL Certificate** > **Add SSL Certificate** > **Custom**
  * Donner un nom arbitraire pour le certificat
  * Choisir le fichier de certificat SSL et sa clé associée

# Nextcloud
```
volumes:
  nextcloud:
  db:

services:
  db:
    image: mariadb:latest
    restart: always
    command: --transaction-isolation=READ-COMMITTED --log-bin=binlog --binlog-format=ROW
    volumes:
      - db:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=password
      - MYSQL_PASSWORD=password
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud_db

  nextcloud:
    image: nextcloud:latest
    restart: always
    ports:
      - 8080:80
    links:
      - db
    volumes:
      - nextcloud_data:/var/www/html
      - nextcloud_apache:/etc/apache2/
    environment:
      - MYSQL_PASSWORD=password
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud_db
      - MYSQL_HOST=db
```
