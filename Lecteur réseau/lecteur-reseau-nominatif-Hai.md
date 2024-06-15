# Lien
https://www.it-connect.fr/comment-monter-un-lecteur-reseau-par-gpo/

# Méthode 1: Connecter un lecteur réseau en GPO
Sur le serveur de fichier srv-fichier, créez un dossier Net-Admin et partagez ce dossier (Partage et Sécurité-NTFS) --> [Différences permissions NTFS et de partage](https://www.it-connect.fr/serveur-de-fichiers-les-permissions-ntfs-et-de-partage/)\
Suivez [le lien](https://www.it-connect.fr/comment-monter-un-lecteur-reseau-par-gpo/) d'instruction pour créer un mappage de lecture pour toutes les OU ou uniquement l'OU souhaitée, par exemple OU Net-Admin.\
Supposons que vous ayez un utilisateur nommé Jean Dupont avec les informations suivantes :
- Nom de compte : jdupont
- Nom complet : Jean Dupont\
Lorsque cet utilisateur se connecte, la variable %username% sera "jdupont".

![Screenshot 2024-03-03 235446](https://github.com/kawaiiineko-website/tutoriels/assets/170332168/3bb93ad1-0cb7-4782-9d7d-d0772f470ce8)

* Mise à jour forcée de la stratégie de groupe  sur PowerShell
```
gpupdate /Force
```
* Tester la GPO à partir d'un poste client: Logoff puis login ou redémarrer

![Screenshot 2024-02-21 170728](https://github.com/kawaiiineko-website/tutoriels/assets/170332168/927c150e-da61-49aa-aaa1-0e5cf27135a0)

# Méthode 2 (manual): Utilisateurs et ordinateurs Active Directory > [Utilisateur] > Properiétés > Profil > Connecter
Sur le fichier de fichier, créez un dossier Net-Admin et partagez ce dossier (Partage et Sécurité)\
Sélectionnez le lecteur\
Sélectionnez le chemin: \\\srv-2012\Net-Admin\\%username%
![Screenshot 2024-02-21 160726](https://github.com/kawaiiineko-website/tutoriels/assets/170332168/8021db96-41cb-4e58-8707-9e43ca7db1f7)
![Screenshot 2024-02-20 165701](https://github.com/kawaiiineko-website/tutoriels/assets/170332168/57b13033-5d50-4cd0-ae28-df501116a4e2)
