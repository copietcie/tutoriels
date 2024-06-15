# Ouverture à l'extérieur

## Etape 1 : Théorie
Prenons ce réseau pour exemple :

![example_ouverture_wan drawio](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/83c482c9-fe91-4004-8284-8c35aae6eab8)

On remarque que : 
* Le poste client et le serveur web ne sont pas sur le même réseau
* Il y a deux pare-feu/routeurs qui se trouvent à l'extrêmité de chacun des deux réseaux
* Ces deux pare-feu/routeurs se trouvent sur le même réseau (donc peuvent se communiquer)

Nous allons donc exploiter cette communication : 
* Le poste client envoie une requête à 192.168.10.2 sur le port 80
* Le poste client ne connait pas ce réseau, il l'envoie à sa passerelle
* Le pare-feu réseau reprend la main mais lui non plus ne connaît pas ce réseau il l'envoie à sa passerelle et ainsi de suite jusqu'à trouver le serveur web
* Sauf que problème, cette requête n'aboutira jamais car c'est une IP classe privée non routée sur Internet.

Pourtant les deux pare-feu sont sur le même réseau pourquoi ça ne passerait pas ? 
* Car la passerelle par défaut du pare-feu qui permet à notre poste client de sortir sur Internet n'est pas le pare-feu de notre serveur web. Donc il y a aurait des bonds jusqu'à jamais trouvé ce serveur.

Que faire ?
* Pour rappel : Les deux pare-feux sont sur le même réseau, donc ils peuvent se communiquer
* Donc si le poste client tente de joindre le second pare-feu (et que tous les flux sont autorisés sur le WAN de ce pare-feu) il devrait pouvoir le joindre.

Comment ça se fait ? 
* Le poste client envoie une requête ICMP à 172.16.0.254/16, sauf qu'il ne connait pas ce réseau, alors il l'envoie à sa passerelle par défaut le premier pare-feu
* Celui-ci reprend la main et regarde s'il connait ce réseau et surtout l'équipement sur ce réseau (SWITCHING), il va alors l'envoyer directement au second pare-feu
* Le second pare-feu va répondre à la sollicitation du premier pare-feu et le premier pare-feu va envoyer sa réponse au poste client et ainsi les requêtes ICMP passent

Nous avons tout ça mais on ne communique toujours pas avec le serveur web...
* C'est là que nous allons utiliser la technique du port forward
* Nous allons faire une règle de Port Forward sur le second pare-feu en lui disant que s'il reçoit une sollicitaition sur le port 80, qu'il doit le rediriger vers la serveur web (qui est dans son réseau LAN)
* De ce fait, lorsque le poste client va tenter de requêter le second pare-feu sur le port 80, celui ci va le rediriger vers le serveur web et ainsi il pourra accéder à son site web par l'extérieur.

## Etape 2 : Pratique
* Maintenant, nous allons changer le port d'écoute WEB du second pare-feu (qui est généralement sur le 80 ou 443 pour pouvoir le configurer avec une interface web)
* System > Advanced 
