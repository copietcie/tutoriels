# Installation de ferme RDS

## Etape 1
* Mettre plusieurs serveurs (1 Broker, 2 RDS)
* Joindre les 3 serveurs dans le domaine
* Sur le Broker ajouter les serveurs RDS (Gestionnaire des serveurs > Gérer > Ajouter un serveur)
* En faire un groupe pour une meilleure gestion (Gestionnaire des serveurs > Gérer > Ajouter un groupe de serveur)

## Etape 2
* Aller dans Gérer > Ajouter un rôle ou une fonctionnalité > Installation des services de Bureau à distance
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/23beb241-796b-4795-a35d-2dff084c6c34)
* Faire "Déploiement standard"
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/a87ea1ae-f170-4916-894f-585e3c6a5dc7)
* Sélectionner "Déploiement basé sur une session"
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/d3426236-a2f8-4c5b-8824-d0a60b1d2920)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/f7c22048-0a94-47d8-ae47-c5455b2e7c19)
* Choisir le serveur qui fera le BROKER
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/a1ab3313-e189-4ec9-82c4-c38bfead91a6)
* Ajouter l'accès WEB sur le broker pour permettre à un client d'accéder à son application via son navigateur
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/a157e122-97f1-44e0-abc4-5fd8f495d48d)
* Sélectionner les serveurs qui seront RDS
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/551cc535-bf1c-4e9a-84ff-841e42d43c6f)




