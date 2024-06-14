# DNS Menteur
Le DNS menteur c'est le fait de modifier le fichier host d'un poste/machine afin de faire la résolution manuellement (sans serveur DNS)
* Sur Windows :
  * **C:\Windows\System32\drivers\etc\hosts** => A ouvrir avec Bloc Note ou Notepad en mode administrateur pour le modifier ou le copier quelque part pour le recoller par dessus dans le même endroit
  * Format : ```IP	DNS``` | ``` 172.16.181.224 nextcloud.myenterprise.com```
* Sur les distributions Linux :
  * **/etc/resolv.conf**, le modifier avec nano ou vim sous le compte root
  * Format : ```IP       DNS ``` | ``` 127.0.1.1       docker-s6```

# DNS Local
C'est le serveur DNS qui sert à faire la résolution de nom dans un réseau interne
Généralement c'est l'AD (qui possède le serveur DNS) ou alors le routeur (PFSense)

Dans ce cas, les enregistrements doivent être fait dans ce serveur là afin de pointer des noms de domaines à des IP (pour des ressources LOCALES)

* Exemple avec **DNS** de l'AD il est possible de faire un domaine particulier :
  * Ouvrir **Gestionnaire DNS** > **Nouvelle zone** > **Zone principale** > (Si AD secondaire, dire où le DNS est répliqué) > Nom de domaine > **N'autoriser que les MAJ dynamiques sécurisées** > Terminer
  * Créer un enregistrement DNS qui pointe vers le bon machine (serveur qui héberge un site généralement) > Nouvel hôte A ou AAAA > FQDN > Mettre l'IP correspondant et valider 

![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/ad3638f8-a9b1-4881-8ba9-27fc1f637e73)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/c5ae2163-feba-4d40-a500-2ebd37fa5573)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/73786844-0416-45ed-ba10-aa7c67cbeb15)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/725f1fb0-e320-4a78-b285-d10245ca57f9)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/f8725866-9469-4ffb-abe3-8df5117d22a3)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/aa7ec11f-bc1b-4a97-b786-2b889ed52842)

![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/5fd2fe8f-8ea4-4d0c-b039-8c3ec7bd0487)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/4a28a2d4-df49-47b9-a515-a7bdb4b2be7a)






