# Ajouter l'authentification LDAP sur Nextcloud

## Etape 1
* Aller sur Nextcloud, cliquez sur l'icône à droite de l'écran (Profil) puis cliquer sur "+ Applications"
* Dans "Vos Applications", activer l'application "LDAP User and Group Backend"
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/b92a424c-ddac-4867-a944-fa8562d5e600)

## Etape 2
Configuration du LDAP
* Aller sur Nextcloud, cliquez sur l'icône à droite de l'écran (Profil) puis cliquer sur "Paramètres d'Application", dans la section "Administration" cliquer sur "Intégration LDAP/AD"
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/6a7c5e1f-8275-4db1-8f91-830c9b8a160a)
* Configurer comme ceci (le conteneur peut communiquer avec l'AD comme son "interface Docker" est en BRIGDE :
  * **Host** : L'IP de l'AD
  * **Port** : 389 (Par défaut)
  * **Compte qui a un accès
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/753dd740-8992-4ed4-8cd7-1958532e77d7)



