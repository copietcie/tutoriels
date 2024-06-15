# Nginx
* Installer Nginx sur une machine Debian
```
apt-get update && apt-get install -y nginx
```


## Etape 2
* Configuration /etc/nginx/sites-available/<nom_conf.conf>
```
upstream backend {
    server IP
    server IP2
}
server {
    listen    80;
    server_name    www.glpi-interne.fr;

   location / {
        include proxy_params;
        proxy_pass http://glpi;
    }
}
```
=> le "upstream" est l'endroit où on indique les différents sites qui seront derrière le proxy
=> server { c'est l'équivalent au vhost sur Apache, on dit que le proxy écoute sur le port 80 sur son ip et le nom de domaine à mettre pour le serveur derrière le proxy. La location / est nécessaire pour dire de faire la "redirection" vers le bon serveur par besoin de mettre l'IP ou le nom de domaine, il suffit de mettre le nom mis au "upstream"
	- Activer la conf: ln -s /etc/nginx/sites-available/X.conf /etc/nginx/sites-enabled/X.conf
	- Restart/reload : systemctl reload nginx
Puis tester.
