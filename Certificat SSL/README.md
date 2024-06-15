# Comment générer un certificat SSL avec sa clé associée
Pré-requis : Le paquet "openssl" doit être installé sur une machine (généralement sur Debian c'est par défaut), il est également disponible sur Windows.

## Faire une arborescence pour stocker la clé et le certificat
```
mkdir /etc/apache2/certs
chown -R www-data:www-data /etc/apache2/certs
```

## Générer le certificat et sa clé associée
```
cd /etc/apache2/certs
openssl req -new -x509 -days 365 -nodes -out <nom_arbitraire>.crt -keyout <nom_arbitraire>.key
```
=> Le .crt est le certificat et le .key la clé, le nom est arbitraire mais pour se retrouver simplement, il est conseillé de mettre le nom de domaine associé au certificat.

## Mettre les droits de propriété sur le certificat et la clé pour que l'utilisateur d'Apache puisse le lire : 
```
chown www-data:www-data <nom_arbitraire>.crt
chown www-data:www-data <nom_arbitraire>.key
```

## Installation du certificat et de la clé sur Apache2
Lancer la commande suivante pour activer le module SSL :
```
a2enmod ssl
```

Editer le fichier vhost correspondant au site web à protéger et le faire écouter sur le port 443 : 
```

```

Redémarrer Apache2 en vérifiant que la conf est bonne (pour éviter que ça ne redémarre plus) : 
```
apachectl -t
systemctl restart apache2 
```

Vérifier qu'Apache est bien démarré 
```
systemctl status apache2
```

## Vérifier
Se rendre sur le site en HTTPS et regarder que le certificat est bien pris en compte : 
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/5d0b7c7d-2b8e-45ff-b763-d00dae06e7c9)

