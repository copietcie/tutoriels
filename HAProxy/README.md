# Installation de HAProxy

## Etape 1

Installer le paquet haproxy 
```apt-get update && apt-get install haproxy```

## Etape 2

Configuration exemple :

Dans le fichier
```
nano /etc/haproxy/haproxy.cfg
```
On peut faire une sauvegarde avant la manipulation

Tout écraser et remplir
```
# add to the end
# define frontend ( any name is OK for [http-in] )
frontend http-in
        # listen on 80 port
        bind *:80
        # set default backend
        default_backend    backend_servers
        # send X-Forwarded-For header
        option             forwardfor

# define backend
backend backend_servers
        # balance with roundrobin
        balance            roundrobin
        # define backend servers
        server             <NOM_DU_SITE_1> <ADRESSE_DU_SITE_1>:80 check
        server             <NOM_DU_SITE_2> <ADRESSE_DU_SITE_2>:80 check
```
Puis redemarrer le haproxy
```
systemctl restart haproxy
```

## Etape 3

Sur les serveurs web, faire sur chacun d'entre eux, la manipulation suivante
```
a2enmod remoteip
```
Aller dans 
```
nano /etc/apache2/apache2.conf
```
Et noter les 2 lignes
```
RemoteIPHeader X-Forwarded-For
RemoteIPInternalProxy <ADRESSE_DU_HAPROXY>
```
A la ligne 212

RemoteIPHeader X-Forwarded-For
RemoteIPInternalProxy 10.0.0.30
LogFormat "%v:%p %a %l %u %t \"%r\" %>s %O \"%{Referer}i\" \"%{User-Agent}i\"" vhost_combined
LogFormat "%a %l %u %t \"%r\" %>s %O \"%{Referer}i\" \"%{User-Agent}i\"" combined

Puis redemarrer le server apache2
```
systemctl restart apache2
```



