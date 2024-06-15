# Bloquer le répertoire /wp-admin
Filtrer le répertoire à certains postes par IP dans le VHOST

```
<VirtualHost *:80>
    Redirect permanent / https://www.domain.tld
</VirtualHost>

<VirtualHost *:443>
    ServerName domain.tld
    ServerAlias www.domain.tld
    DocumentRoot /var/www/html
    SSLEngine on
    SSLCertificateFile /opt/certif/certificat.crt
    SSLCertificateKeyFile /opt/certif/certificat.key
    <Directory /var/www/html/wp-*>
      Require ip 192.168.0.5 127.0.0.1
      Require all denied
    </Directory>
    <Directory /var/www/html>
      AllowOverride All
      Require all granted
    </Directory>
</VirtualHost>
```
