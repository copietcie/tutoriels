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
  * **Compte qui a un accès** (faire un compte en ro sur l'AD) : Exemple : cn=nextcloud-ro,ou=Informatique,dc=myenterprise,dc=com
  * **Mot de passe du compte qui a l'accès à l'AD** :
  * **Base DN** : La forêt au plus haut point pour avoir tous les utilisateurs et filtrer ensuite
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/753dd740-8992-4ed4-8cd7-1958532e77d7)
  * Faire "Suivant"

* Mettre sur "person" et "user"
* Filtrer sur des groupes (il faut cliquer sur les groupes puis cliquer sur le petit crocodile pour le prendre en compte)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/762243e9-d3e1-4f1a-97ae-47635537f2bc)
* ça donnera un filtre et on peut **Vérifier et compter les utilsateurs** pour voir combien il y a d'utilisateurs

* Ce qui est utilisé pour l'authentification
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/8a6237ec-60ad-41ce-9393-3638a33ac694)

* Possibilité d'ajouter également des groupes de l'AD dans le Nextcloud
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/9b5eb58c-3b3e-41dd-99d9-121c2eae2455)

## Etape 3
Vérifier que les utilisateurs et les groupes sont bien remontés :
* Aller sur Nextcloud, cliquez sur l'icône à droite de l'écran (Profil) puis cliquer sur "Utilisateurs"
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/ba5ab8b6-0092-4e57-9c65-630c9253f2e3)









