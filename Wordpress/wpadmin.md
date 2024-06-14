# Bloquer le répertoire /wp-admin
Filtrer le répertoire à certains postes 
dans le fichier .htaccess placer dans /var/www/html/wp-admin

copier le texte suivant
(texte à adapter au contexte)

```
<Limit GET POST PUT>
order deny,allow
deny from all
# IP d'Alex
allow from xxx.xxx.xxx.xxx
# IP de Nico
allow from xxx.xxx.xxx.xxx
# IP d'un autre point d'accès
allow from xxx.xxx.xxx.xxx
</Limit>
```
