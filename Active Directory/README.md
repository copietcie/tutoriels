# Pré-requis pour installer un AD
* Nommer la VM de manière cohérente
* Mettre une IP fixe à la VM
* Ajouter le rôle ADDS

## Faire un AD secondaire
* Nommer la seconde VM de manière cohérente
* Mettre une IP fixe à la VM et ajouter le DNS de l'AD principal en DNS Principal
* Ajouter le serveur secondaire dans l'AD avant d'ajouter le rôle ADDS
* Ajouter le rôle ADDS et retirer le Serveur DNS mais garder le catalogue 
* Faire promouvoir ce contrôleur de domaine
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/d1ebcf8a-eaa4-4641-9cb5-26c0cc38e97d)
* Faire ajouter un contrôleur de domaine dans un domaine existant
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/94cbace7-5104-4018-bac6-ba88c1001c48)
* Bien retirer "Serveur DNS"
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/68f595bc-89b7-4bef-b9e6-9f2ff9916735)
* Sélectionner le bon serveur AD à répliquer
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/7c39a248-26b2-43e0-a241-699077a27ffb)
* Ouvrir "Sites & services ActiveDirectory" si un second site existe sur un autre subnet, passer le temps de réplication au plus minimum
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/27b6139d-b830-4e08-b0d1-a7b2733e561f)
* Lorsque c'est intra-site, la réplication est immédiate, il faut juste rouvrir le "Utilisateur et Services Active Directory"
* Commande pour répliquer les objets AD du maître aux autres :
```
repadmin /syncall /AdeP
```

