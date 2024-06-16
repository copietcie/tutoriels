# Checkpoints - Les points de contrôle
## Lien
* https://learn.microsoft.com/fr-fr/virtualization/hyper-v-on-windows/user-guide/checkpoints
* https://www.it-connect.fr/les-points-de-controle-avec-hyper-v/ \
Checkpoints permet de capturer l'état d'une VM à un instant donné, vous permettant de rétablir ultérieurement cet état si nécessaire.
![image](https://github.com/kawaiiineko-website/tutoriels/assets/170332168/dd5ae776-bc64-4752-a02b-63e295418536)

## Quand Créer des Checkpoints 
Avant les changements importants, mises à jour, mises à niveau, ou dans le cadre des opérations de sauvegarde.

## Deux types différents de points de contrôle
![image](https://github.com/kawaiiineko-website/tutoriels/assets/170332168/31146504-8ae5-4d89-995e-dba8e9568eeb)

* **Points de contrôle standard** : une capture instantanée de la machine virtuelle et de l'état de sa mémoire est prise lors de l'initiation du point de contrôle. Une capture instantanée n’étant pas une sauvegarde complète, il peut entraîner des problèmes de cohérence des données avec les systèmes qui répliquent les données entre différents nœuds (comme Active Directory). Avant Windows 10, Hyper-V offrait uniquement des points de contrôle standard (anciennement nommés captures instantanées).

* **Points de contrôle de production** : ils utilisent le service VSS (Volume Shadow Copy Service) ou File System Freeze sur une machine virtuelle Linux pour créer une sauvegarde cohérente des données de la machine virtuelle. Aucune capture instantanée de l’état de la mémoire de la machine virtuelle n’est prise.

Si vous avez sélectionné Points de contrôle standard, vous pouvez activer la fonctionnalité Points de contrôle automatiques, qui prend automatiquement des points de contrôle des machines virtuelles lorsqu'elles sont démarrées et les supprime dès qu'elles sont arrêtées.
## Checkpoints Automatiques vs Manuels 

Les checkpoints automatiques sont utiles mais peuvent poser des problèmes de stockage et de performance ; les checkpoints manuels sont meilleurs pour les environnements contrôlés.

Vous pouvez utiliser le script PowerShell pour créer un checkpoint **quotidien** programmé pour une VM Hyper-V et gérer les anciens checkpoints en les supprimant après **un certain nombre de jours** (ex: 7 jours) .. Programmer le Script avec le Planificateur de Tâches.

## Maintenance Régulière 
Surveillez et nettoyez régulièrement les anciens checkpoints pour éviter des problèmes de stockage et de performance.
