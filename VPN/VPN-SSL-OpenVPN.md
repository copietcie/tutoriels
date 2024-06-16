# Faire un VPN Nomade


## Etape 1 : Création d'une autorité de certification 

Cette autorité va notamment servir à faire des certificats auto-signés pour notre VPN-SSL.
Il faut tout d'abord la créé : 

* Se rendre dans **System** > **Certificate** > **Onglet Authorities** puis cliquer sur le bouton **Add**
Donner un nom graphique / descriptif pour l'autorité de certification 

<image>

* Mettre "Create an internal Certificate Authority"
* Changer le **Lifetyme (days)** à 365 jours.
* Donner un FQDN à l'autorité de certification (exemple : vpn.myenterprise.com) => C'est le nom utilisé pour générer le certificat
* Le reste en bas est facultatif mais peut être rempli.

<image>

## Etape 2 : Création d'un certificat serveur
Il permet de vérifier que le client qui tente de se connecter a bien le bon certificat signé par la bonne autorité de certification (ici le pare-feu) et s'assure de valider ou non la connexion

* Se rendre dans **VPN** > **System** > **Certificate** > Onglet **Certificate**
* Choisir dans **Method** : Create an internal Certificate
* Donner un nom descriptif arbitraire
* Changer le **Lifetyme (days)** à 365 jours.
* Donner un FQDN au certificat (on peut garder le même que pour l'autorité de certification)
* Dans **Certificate Attributes** changer **Certificate Type** à "Server Certificate"
* Faire **Save**

## Etape 3 : Authentification LDAP sur un groupe précis 
* Sur l'AD créer un groupe de sécurité avec un nom voulu et y mettre dedans les personnes qui sont autorisées à se connecter en VPN
* Récupérer son DN (Clic droit sur le groupe > Propriétés > Editeurs d'attributs > dinstinguishedName)
* Créer un utilisateur pour pfsense pour qu'il puisse récupérer les informations des utilsateurs sur l'AD, même chose, récupérer son DN
* Se rendre sur PFSense > System > User Manager > Authentication Servers > Add
Exemple de configuration :
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/c94c92bf-9826-4645-a295-59cfa50845a4)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/b1fa270c-155f-4c02-a45c-326fefe73a7b)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/24372e31-f98e-42d5-a6f7-32c57ff68ba9)

* Sauvegarder et tester la connexion (Diagnostic > Authentification) => Le compte utilisé pour le test doit être membre du groupe créé précédemment
* Changer le serveur d'authentification par l'AD (System > User Manager > Settings > Authentification Server)

* Créé un utilisateur qui va seulement servir à utiliser le certificat SSL (System > User Manager > Add)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/12443e50-3e97-4b4f-9278-7a9d7a240c50)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/f0784e5c-63a8-4f5c-b997-773d05369171)

## Etape 4 : Configuration du serveur OpenVPN
* Se rendre dans VPN > OpenVPN > Servers et Add
* 
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/0714ef31-1d8a-443f-a45f-872e0d113c38)
*
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/8c6dc33a-eded-4c12-81a8-841860552f64)
*
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/1b186ad3-7657-4527-b8fa-bc5265780b2d)
*
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/6bd8c93c-86fc-4a0f-bdb3-7f015c495ba3)
*
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/8281453d-5ec7-48fd-b9ce-0b4d014a3503)
*
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/edc81fd1-a374-4f62-9c5a-6d2ed908c3d8)
*
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/bb648e0a-cf10-4c01-939e-72aab30cc589)

* Pour lui faire utiliser le DNS local si besoin de se connecter à des sites internes
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/61e24ee4-47d5-4f05-9c24-46f1165c468e)


## Etape 5 : Installation du client export pour OpenVPN
* Se rendre dans : System > Package Manager > Available Packages
* Rechercher openvpn et installer openvpn-client-export
* Configurer le client export si besoin (VPN > OpenVPN > Client Export)
* Descendre tout en bas et récupérer la conf ovpn de l'utilisateur fait pour tout le monde (Inline configuration > Most Clients)


## Etape 6 : Autoriser les flux
* Autoriser les flux sur le WAN à destination du port 1194
* Ajouter des règles sur l'interface OpenVPN pour autoriser le client VPN à communiquer avec les ressources du réseau

## Etape finale : Tester
* Installer OpenVPN sur un poste sur un réseau externe : https://openvpn.net/community-downloads/
* Importer la configuration téléchargée précédemment et lancer la connexion (des logins sont demandés, utiliser un compte AD qui est membre du groupe VPN)
* Lancer la connexion et tenter d'accéder aux ressources internes

Source : https://www.it-connect.fr/pfsense-configurer-un-vpn-ssl-client-to-site-avec-openvpn/
