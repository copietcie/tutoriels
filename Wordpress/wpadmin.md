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
    <Directory /var/www/html/wordpress/wp-*>
      Require ip X.Y.Z.A 127.0.0.1
      Require all denied
    </Directory>
    <Directory /var/www/html>
      AllowOverride All
      Require all granted
    </Directory>
</VirtualHost>
```

![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/59c4bf78-a1ba-41f9-8d33-e7e699f2d7df)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/e01b6809-a093-4cd4-b138-f95b5f9f43f1)

