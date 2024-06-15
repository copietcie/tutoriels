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
* Installer la passerelle Gateway RDS
* Se rendre dans "Gestionnaire de serveur" > "Service de bureau à distance" > "Vue d'ensemble" > "Tâche" > "Modifier les propriété de déploiement"
* Sur la fenêtre qui s'ouvre descendre un peu et cliquer sur "Créer un certificat"
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/2dac6c30-9203-4fe2-841c-849062e8ea20)
* Donner le nom FQDN du broker (trouvable sur le DNS de l'AD) et mettre un mot de passe (pour le certificat)
* Stocker le certificat quelque part
* Et cocher la case d'autorisation
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/9ba9721e-436a-4f4c-8b83-0e3c425a984c)

* Mapper le certificat sur l'ensemble des serveurs (Broker et RDS) (Sélectionner un certificat existant > Parcourir et mettre le bon certificat et appliquer à chaque fois à la fin tout doit être en "OK")
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/1f27b71b-d5a2-443d-8543-d2ec985910fb)


## Etape 5
Une fois que le certificat est installé sur l'ensemble des serveurs, il est temps d'accéder au broker par un navigateur web pour avoir le bon raccourci : 
* Se rendre sur le poste du client (Windows client joint dans le domaine)
* Ouvrir un navigateur et taper "https://nom_de_domaine/Rdweb
* Se connecter avec un compte dans le bon groupe (Compte ou informatique) et vérifier que c'est bien le bon raccourci qui est proposé à télécharger et ensuite lancer le raccourci et se connecter
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/d25a8b2e-ee66-4872-a66d-4d6ec8d73d15)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/9b316a5a-ef60-497e-a6ce-325e13516e78)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/7c902ad9-fa39-426f-ac61-6c650e7589f2)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/35755dbb-37ab-411e-be7b-50b1ea043748)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/6251aa75-d5a5-42cd-95a3-02c9b193f364)
* On attérit bien sur le bon RDS
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/bd3a5093-ea2d-46c9-92e4-a4fa345a0872)
o


