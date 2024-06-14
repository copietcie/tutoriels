# Installation Veeam
Tutoriel pour Veeam CE
Il est possible de sauvegarder 10 machines différentes en version CE et 1 tâche de sauvegarde = 1 CPU donc bien le dimensionné si plusieurs tâches de sauvegardes sont lancées en même moment
Minimum : 2CPU / 2048 Go

## Etape 1
Récupérer l'ISO en s'inscrivant sur Veeam (VBR)

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
* Il demande à quel serveur VBR on veut connecter, ici c'est le serveur lui même qui fait office de sauvegarde et console, donc laisser tout par défaut et mettre un compte apte à se connecter à ce serveur avec des droits administrateurs (ici Admin local mais un admin du domaine peut aussi) en cochant la case il est possible d'utiliser la session en cours pour lancer la console :
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/6a465034-50e1-400a-b5a7-a0e5400159ce)
=> Si le serveur a été redémarré, ça prend un peu de temps à se relancer, donc attendre un peu avant de tenter une connexion

### Changement de repo de sauvegarde (FACULTATIF)
* Par défaut, les sauvegardes sont stockés dans C:\Backup, il est possible de le changer :
* Aller dans "Backup infrastructure" > Backup repository > Clic droit > Add "Backup Repository" > Choisir le type de disque (partage, sur une VM, etc..), un assistant s'ouvrira
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/e225ab7f-82b9-4664-8f92-2587c974108d)
* Sélectionner le serveur de dépôt de sauvegarde (ici c'est la machine elle même, si c'est une autre machine faire "Add new" et suivre les instructions d'ajout) et faire "Populate" pour avoir les disques (ici on utilise E:\)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/705ed91f-0953-48e4-837e-46a9f20e3945)
* Donner l'endroit exact où on veut sauvegarder sur le disque (ici ça sera par défaut, mais utiliser "Browse" pour changer de répertoire) et adapter les paramètres "Concurrent task" = nb de tâche de sauvegarde en simultanées autorisées : 
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/9e0db7be-8564-42aa-9e39-469aedbfb779)
* Ignorer la recommandation
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/33e5de0f-44b3-4a20-8839-5701e54a3fbd)
* Décocher le vPowerNFS (permet de faire des restaurations entière de VM pour les hyperviseurs VMWare, ici nous sommes sur Hyper V et ce n'est pas inclus)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/974703ca-2f0b-49e9-b419-0ba0fa3358e7)
* Laisser par défaut et Appliquer :
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/1f9ef45e-f6a2-477d-b58e-e5e178a0c9eb)
* Regarder que tous les vvoyants sont verts :
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/277d769a-1cf7-4c84-a134-3c74f77d3ca1)
* Confirmer le changement de répertoire de sauvegarde par défaut vers le nouveau répertoire créé :
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/b03d6263-5ac5-4a76-b283-0c11c5f79eb7)

### Ajout de l'hyperviseur Hyper-V dans l'inventaire de sauvegarde (Facultatif)
* Faire "Inventory" > Virtual Infrastructure > Add Server > Choisir "Microsoft Hyper V"
* Sur l'assistant qui s'ouvre, ajouter l'IP ou le nom de la machine Hyper V (faire attention, vérifier que l'hyperviseur communique avec la VM Veeam, si c'est du réseau interne, il y a une carte réseau virtuelle qui peut être mis dans le même réseau que le réseau interne et si un DHCP est conf c'est auto)
* On choisit "Standalone" car c'est un seul Hyper V
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/806baac3-6ff0-42b8-86c1-3de741e867eb)
* Dans les credentials il faut mettre un utilisateur avec les droits administrateurs sur l'Hyper V (si l'hyper V n'est pas dans le domaine, mettre le compte local), faire "Add" pour en ajouter un utilisateur sous la forme NOM_PC_LOCAL\Utilisateur ou DOMAINE\Utilisateur)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/7e8dae83-a766-47e6-bd83-e4d52d18918d)
Continuer jusqu'à réussir.

### Création d'un job de sauvegarde
* Aller dans "Home" > Clic droit et choisir "Virtual machine" **(Seulement si la partie au dessus a été faites)**
* Sinon faire "Home" > Clic droit et choisir "WIndows MAchine" ou "Linux Machine" (à adapter selon l'OS à sauver)

* Sélectionner "Server" et "Managed by Backup Server"
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/5dd79f43-4c06-48bc-8a96-1b07d8d28349)
* Nommer le job de backup
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/58a21e59-95c9-4e9e-9465-56a5a7e2b2c4)
* Ajouter la cible à sauvegarder et un compte administrateur qui a les droits dessus (un admin du domaine marche):
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/226f60b4-3178-45cd-b233-fc828da242f9)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/73589b8c-dcdc-445a-be99-b9e6529218de)
* Sélectionner le mode de sauvegarde (ici la sauvegarde ENTIERE de la VM est sélectionnée) :
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/a5c5606c-7dbd-4e4f-98a2-2b580214f3bb)
* Choisir le répertoire de sauvegarde (qu'on avait mappé au début) puis la rétention (nb de jours où les sauvegardes sont gardés ou en points de restauration)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/e31b2397-3922-4bbe-b033-e9b270b70a51)
* Pour une meilleure personnalisation de la sauvegarde (incrémentielle / totale) on peut cliquer sur Advanced pour changer :
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/8e8c8508-0126-43a2-bd85-cae16acb9d3f)
* Sur la fenêtre suivante, laisser la case cochée par défaut, on peut ajouter l'indexation de fichier et le scan de malware sur la sauvegarde (Attention on peut mettre une indexation sur tous les fichiers de la cible à sauvegarder)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/0b717ccc-318a-4b4d-81d5-b67f78d2dedb)
* Planifier le job de sauvegarde et dire après combien de fois il peut essayer si erreur :
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/42a4c004-05eb-4395-8ce6-c740d473890b)
* Pour le test il est possible de forcer le job de sauvegarde en cochant "Run the job after closing"
* Attendre un peu et si tout est OK, ça doit apparaître dans "Sucess"
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/0a761a81-df9c-4e32-a571-8a66c5a0eb5d)
Sinon checker les erreurs et voir ce qui ne va pas


### Restauration d'une sauvegarde (PRA)
* On peut faire une restauration d'une sauvegarde entière d'une VM
* On peut égalemement avoir restaurer par exemple "une partie" comme un dossier et des fichiers particuliers (activer le file indexing sur tout au préalable)

Pour se faire : 
* Ouvrir Veeam & Backup Replication Console puis aller dans "Home" puis "Backups" et "Disks"
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/4015fc2b-6690-4acf-8397-c4bb4a17bad1)
* Dans la partie de droite, déroulez le job souhaité (ici Backup_AD) puis cliquer droit sur le nom de la VM et choisir entre "Instant Recovery" |=> Il faut configurer la partie **Ajout de l'hyperviseur Hyper-V dans l'inventaire de sauvegarde (Facultatif)**] ou "Restore Guest file"
* Instant recovery => Remet les données de la machine entière à l'état de la sauvegarde
* Restore Guest File => Permet d'avoir de la granularité et de ne restaurer que ce qui est nécéssaire (exemple un fichier malencontreusement supprimé ou plusieurs)

* Dans les deux cas, voici comment les premières étapes se déroulent :
  * Choix de la sauvegarde à remonter
  ![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/745d6785-d440-4e7f-b44c-84f249ff37b8)
  * Donner une raison à la restauration (traçabilité)
  ![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/eaac7575-33c6-4bd3-9c90-59b9a3dafc66)
  * Faire "Restore" pour restaurer une VM entière ou "Browse" pour choisir un ou plusieurs fichiers à restaurer (granularité)

Exemple pour un fichier à restaurer (Clic droit > Restore > Overwrite ou Keep) : 
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/f34aeca5-3ea7-4ac1-8fd7-736f65b4d679)
* Possibilité de réécrire par dessus le fichier en production (Overwrite) ou bien de faire une "version 2" (keep) pour ne pas perdre la version actuelle
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/6d199c5a-5ceb-4f19-a50f-26c55a8aaa66)


