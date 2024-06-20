# DFS
* Installer Espace de nom sur les serveurs AD
* Installer DFS Réplication sur les cibles DFS (serveurs de fichiers)
* Configurer un espace de nom avec des dossiers et la bonne arborescence sur l'AD 1
* Configurer les dossiers partagés sur les cibles DFS
* Configurer les cibles aux dossiers depuis l'AD 1
* Configurer le groupe de réplication entre les deux cibles DFS

# Les droits
* NTFS => Droit par défaut de Windows gérable dans l'onglet "Sécurité" d'un fichier/répertoire
* Partage => Droit octroyé à un partage dans l'onglet "Partage" puis "Autorisation"
Les droits les plus restrictifs sont appliqués, exemple : "Lecture pour tout le monde sur NTFS VS Modification pour tout le monde sur Partage" => C'est la lecture qui sera appliquée
