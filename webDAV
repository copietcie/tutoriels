Un protocole que Nextcloud utilise pour faire serveur de fichier et par exemple on peut ouvrir Nextcloud de l'extérieur.

Pour le webDAV avec IIS de Microsoft et le DFS

Il est possible de configurer deux instances de DFS (Distributed File System) synchronisées et d'utiliser WebDAV pour y accéder. Voici un guide étape par étape pour configurer cette architecture sur un Windows Server :
Configuration de DFS Répliqué

    Installer le rôle DFS sur les serveurs :
        Ouvrez le Gestionnaire de serveur.
        Cliquez sur Ajouter des rôles et fonctionnalités.
        Sélectionnez Rôle de serveur puis Services de fichiers et de stockage > Services de fichiers et iSCSI > DFS Namespaces et DFS Replication.

    Configurer le Namespace DFS :
        Dans le Gestionnaire de serveur, allez à Outils > Gestion DFS.
        Faites un clic droit sur Namespaces et sélectionnez New Namespace.
        Suivez l'assistant pour créer un nouveau namespace DFS, spécifiant le serveur et le nom du namespace.

    Configurer la Réplication DFS :
        Toujours dans Gestion DFS, faites un clic droit sur Replication et sélectionnez New Replication Group.
        Choisissez Multipurpose replication group et suivez l'assistant pour ajouter les serveurs de réplicas et les dossiers à répliquer.

Configuration de WebDAV
Installer le rôle WebDAV :
        Ouvrez le Gestionnaire de serveur.
        Cliquez sur Ajouter des rôles et fonctionnalités.
        Sélectionnez Rôle de serveur puis Serveur Web (IIS) > Services de rôle > WebDAV Publishing.

    Configurer WebDAV dans IIS :
        Ouvrez Gestionnaire des services Internet (IIS).
        Sélectionnez votre site web ou créez un nouveau site.
        Dans le panneau Actions, cliquez sur Activer WebDAV.
        Cliquez sur WebDAV Authoring Rules pour définir les règles d'autorisation.
        Cliquez sur Add Authoring Rule et configurez les permissions pour les utilisateurs ou groupes nécessaires (lecture, écriture, etc.).
Configurer les Répertoires Virtuels pour DFS :
        Dans le Gestionnaire des services Internet (IIS), faites un clic droit sur votre site web et sélectionnez Ajouter un répertoire virtuel.
        Pointez le répertoire virtuel vers le chemin UNC du DFS namespace (par exemple, \domain\dfsnamespace).

Synchronisation et Accès via WebDAV

    Vérification de la Réplication DFS :
        Assurez-vous que les dossiers spécifiés pour la réplication DFS sont bien synchronisés entre les deux serveurs.

    Tester l'Accès WebDAV :
        Depuis un navigateur web ou un client WebDAV (comme NetDrive ou Cyberduck), tentez de vous connecter à votre site WebDAV.
        Utilisez l'URL du site IIS avec WebDAV (par exemple, http://votre-serveur/webdav) et authentifiez-vous avec les informations d'identification appropriées.

    Sécurisation de l'Accès :
        Configurez SSL pour sécuriser les communications WebDAV en suivant l'assistant Certificats de serveur dans IIS.
        Appliquez des politiques de sécurité et des groupes d'utilisateurs pour contrôler l'accès aux fichiers partagés.

Conclusion

Cette configuration permet à vos utilisateurs d'accéder à un DFS répliqué via WebDAV, en combinant les avantages de la réplication et de la gestion centralisée des fichiers de DFS avec la flexibilité d'accès offerte par WebDAV. Voici un résumé des étapes clés :

    Installer et configurer DFS et la réplication DFS sur vos serveurs Windows.
    Installer et configurer WebDAV dans IIS pour accéder aux namespaces DFS.
    Vérifier la réplication et tester l'accès WebDAV.

Avec cette configuration, les utilisateurs peuvent accéder aux fichiers de manière transparente et sécurisée, même en dehors de votre réseau local.
