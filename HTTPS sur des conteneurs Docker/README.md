# HTTPS sur des conteneurs Docker

Il n'y a pas besoin si le certificat est mis en amont sur le reverse proxy (NGINX PROXY MANAGER) => https://github.com/kawaiiineko-website/tutoriels/tree/main/Docker%20%26%20Haute%20disponibilit%C3%A9

Sinon, il faudra mettre de la persistence sur les conteneurs notamment dans le répertoire /etc/apache2 pour avoir les confs pour toujours et les modifier simplement sans qu'un redémarrage les écrase.
Si mes manifestes Docker compose sont utilisés pour la création des stack de conteneurs, alors il y a déjà de la persistence dessus => https://github.com/kawaiiineko-website/tutoriels/tree/main/Docker%20%26%20Haute%20disponibilit%C3%A9

## Etape 1 

* Se connecter sur la VM qui fait du Docker

* Lister les volumes
``` docker volume ls ```

Ou

``` ls /var/lib/docker/volumes/  ```

=> Noter le nom, si vous utilisez mes manifeste sans changer les nom ça ferait un truc comme ça X_Y_apache
* Aller dans /var/lib/docker/volumes/<nom_de_la_stack>_apache/_data

``` cd /var/lib/docker/volumes/<nom_de_la_stack>_apache/_data ```

* Lister ce qu'il y a avec les droits :
``` ls -l ```

* Faire un répertoire pour accueillir les certificats pour les sites :
``` mkdir certs ```

* Générer les certificats dedans
``` openssl req -new -x509 -days 365 -nodes -out <nom_arbitraire>.crt -keyout <nom_arbitraire>.key ```

* Modifier directement le fichier VHOST dans le répertoire sites-enabled/000-default.conf
Exemple :
```
<VirtualHost *:80>
        Redirect permanent / https://nom_de_domaine.tld
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
<VirtualHost *:443>
        DocumentRoot /var/www/html
        SSLEngine On
        SSLCertificateFile /etc/apache2/certs/<nom_arbitraire>.crt
        SSLCertificateKeyFile /etc/apache2/certs/<nom_arbitraire>.key
</VirtualHost>
```
* Redémarrer le conteneur via Portainer ou en CLI (si vous utilisez mes manifest, les ports 443 sont déjà ouverts) sinon ajouter un nouveau port pour le 443.
