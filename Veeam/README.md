# Installation Veeam
Tutoriel pour Veeam CE
Il est possible de sauvegarder 10 machines différentes en version CE et 1 tâche de sauvegarde = 1 CPU donc bien le dimensionné si plusieurs tâches de sauvegardes sont lancées en même moment
Minimum : 2CPU / 2048 Go

## Etape 1
Récupérer l'ISO en s'inscrivant sur Veeam (VBR + Agent)

## Etape 2
Installer un serveur Windows et l'ajouter au domaine

## Etape 3
* Ajouter le fichier ISO (disque) du Veeam VBR sur la VM (Media > Lecteur de DVD > Insérer un disque)
* Lancer le setup qui est fourni dans le disque
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/325c8834-76d7-48e2-9e1f-bdcb6ef9719a)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/849a8c91-514c-46d3-aba5-6725c784cbb5)
* Cliquer sur "Install Veeam Backup & Réplication" => ça installe VBR + le composant "console" qui permet de gérer graphiquement les sauvegardes, les backup repository, etc...
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/9dabc56f-564d-4063-9c7b-a5658074d3e1)
* Accepter les termes de contrat
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/d7435158-6104-4d44-b851-dc033ab04e33)
* Garder la case coché sur "Update automatically" c'est obligatoire pour la version CE / Gratuite
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/868a6dac-ce8b-4927-aa5c-8601c7bcf2ca)
* Les pré-requis sont en train d'être installé, il faut attendre un peu
* Laisser tout par défaut et noter les ports pour autoriser au filtrage et faire "Install"
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/e31c595e-1d20-4a9d-b74a-dfb2ca8c1609)
* Quand l'installation s'est bien terminée :
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/3c82e855-2104-4f3c-97b6-a19aebd30522)

## Etape 4
Configuration de Veeam 
* Un raccourcis sur le bureau doit être présent, il faut l'ouvrir
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/05168ab5-949d-4934-86fc-ba24fb552299)



