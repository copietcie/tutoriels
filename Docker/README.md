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
  *  
