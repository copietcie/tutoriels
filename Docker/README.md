# Installation de Portainer avec Docker Compose
* Script d'installation de Docker
```
#!/bin/bash
# Add Docker's official GPG key:
  apt-get update
  apt-get install ca-certificates curl
  install -m 0755 -d /etc/apt/keyrings
  curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
  chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/deb>  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
    tee /etc/apt/sources.list.d/docker.list > /dev/null
  apt-get update
```
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
Pour le lancer : 
```
docker compose -f <name_of_the_yml_file.yml> up -d
```
Pour check la conf du compose : 
```
docker compose -f <name_of_the_yml_file.yml> config
```

