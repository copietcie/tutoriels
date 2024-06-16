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
* 



* Changer le **Server Mode** à Remote Access (SSL/TLS + User Auth) => Permet l'authetification par certificat et mot de passe
* Laisser "Endpoint COnfiguration" sur la configuration par défaut, comme la porte d'entrée du VPN est la WAN du PF et le port on laisse pareil

