# Installation de ferme RDS

## Etape 1
* Mettre plusieurs serveurs (1 Broker, 2 RDS)
* Joindre les 3 serveurs dans le domaine
* Sur le Broker ajouter les serveurs RDS (Gestionnaire des serveurs > Gérer > Ajouter un serveur)
* En faire un groupe pour une meilleure gestion (Gestionnaire des serveurs > Gérer > Ajouter un groupe de serveur)
* Sur l'AD penser à faire une gestion des utilisateurs dans les différentes UO par Groupes

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
* Cocher "Redémarrer si nécessaire" et confirmer le déploiement :
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/2fdae967-7df1-43b1-ac2a-b587f751c431)
* Une fois que c'est bien installé voici ce que ça affiche :
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/81c77272-3610-4726-a87d-c1b33448f6a5)

## Etape 3
* Se rendre sur le BROKER et ajouter une collection de session
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/34f6b093-3240-41e2-b5f0-9b8597681930)
* Donner un nom à la collection
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/6b14ef1a-cf52-47b0-8209-bf503e29f2f8)
* Ajouter le serveur qui accueille la collection
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/1a3f2c5d-a873-408e-8914-0918e4657792)
* Ajouter le groupe qui pourra se connecter à cet hôte
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/f0f6b5bf-cb1f-49d7-85fe-cc6105834acc)
* Ajouter un disque utilisateur s'il y a besoin de stocker les données utilisateurs (bureau/appdata/etc) et spécifier la taille max d'un dossier utilisateur => Le répertoire doit être partagé
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/9d270542-2ebc-4a7e-ad50-9cb14e0cda3d)
* Faire "Créer"
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/c5228516-6d44-47eb-b255-502c76f1ffa4)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/dca45e8e-5207-4cd6-be0b-641ca839261e)

## Etape 4
* Installer la passerelle RDS (Vue d'ensemble > Passerelle RDS > Cliquer dessus ça ouvre l'assistant > Lancer l'installation en sélectionnant le serveur puis en rajoutant son nom FQDN)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/e962ae41-23f1-4c51-9c30-c8b76833e08d)





