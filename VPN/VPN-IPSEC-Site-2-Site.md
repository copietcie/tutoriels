Source : https://www.it-connect.fr/vpn-site-to-site-ipsec-entre-deux-pfsense/

# Faire du IPSec entre 2 PF

![ipsec drawio](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/6baef7a2-d0df-4676-a7d5-76ae1cf0a15f)


## Etape 1
* Aller sur le premier PF (PF DE GREGWARE) et cliquer sur "VPN" puis "IPSEC"
* Cliquer sur le bouton "Add P1"
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/b4b09514-2630-4ea9-a954-cdd6b1fabf52)
* Configurer l'IP du PF distant sur lequel le PF1 peut communiquer (par rapport au schéma : 172.16.1.254)
* Dans la partie Phase 1 Proposal, générer une PSK et la copier (elle servira pour le second PF)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/e4a06fa0-ee20-4f11-916f-21d85da1c953)
* Sauvegarder en laissant tout par défaut

## Etape 2 
* Aller sur le premier PF (PF DE GREGWARE) et cliquer sur "VPN" puis "IPSEC"
* Sous la phase 1 que nous avons configuré nous avons un bouton "Add P2"
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/0f5e5e6f-d5a5-4d6b-bad6-dee492e89a54)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/0403ff34-2ba8-4b40-9e48-c25cac565975)
* Cliquer dessus et dire dans "Remote" le réseau LAN du PF deux (selon notre schéma : 10.0.0.0/16)
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/32c28dc5-47aa-4085-8abd-40e8a17bf903)
* Sauvegarder en laissant tout par défaut

**Refaire exactement les mêmes choses sur le PF2 en adaptant l'ip distant du PF1 et son réseau LAN et au niveau de la phase 1 **Phase 1 Proposal** Coller la même PSK copié au dessus**

## Etape 3 
* Dans Firewall -> Rules -> Aller dans IPSEC -> Et autoriser tout (ou filtrer)
* Dans Firewall -> Rules -> Aller dans WAN -> Et autoriser tout (ou filtrer)

## Etape finale 
* Aller dans Status -> IPSec -> et regarder qu'il y a bien nos conf sur les 2 PF
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/5e35dd80-9ca3-4c70-ab10-504163082efe)

* Lancer la connexion de la phase 1 (et si ça passe) faire la phase 2.

Ce que ça doit donner : 
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/7aa46f57-53e7-44dc-bec2-237f6be4076e)

* Tester ensuite le ping par exemple entre une machine dans le LAN du PF1 et une autre machine dans le LAN du PF2
