1. Installation de Keepalived

Sur les systèmes basés sur Debian/Ubuntu :

bash

sudo apt update
sudo apt install keepalived

Sur les systèmes basés sur Red Hat/CentOS :

bash

sudo yum install keepalived

2. Configuration de Base de Keepalived

La configuration de Keepalived se fait via le fichier /etc/keepalived/keepalived.conf.
a. Failover avec VRRP

L'exemple suivant montre comment configurer un basculement simple avec une adresse IP virtuelle partagée entre deux nœuds (un master et un backup).

Fichier : /etc/keepalived/keepalived.conf

Sur le nœud MASTER :

bash

global_defs {
   router_id MASTER
}

vrrp_instance VI_1 {
    state MASTER
    interface eth0
    virtual_router_id 51
    priority 100
    advert_int 1
    authentication {
        auth_type PASS
        auth_pass secret
    }
    virtual_ipaddress {
        192.168.0.100
    }
}

Sur le nœud BACKUP :

bash

global_defs {
   router_id BACKUP
}

vrrp_instance VI_1 {
    state BACKUP
    interface eth0
    virtual_router_id 51
    priority 90
    advert_int 1
    authentication {
        auth_type PASS
        auth_pass secret
    }
    virtual_ipaddress {
        192.168.0.100
    }
}

    router_id : Identifie de manière unique chaque routeur pour VRRP.
    state : Définit si le nœud commence comme MASTER ou BACKUP.
    interface : L'interface réseau à utiliser.
    virtual_router_id : Un identifiant VRRP unique sur le réseau.
    priority : La priorité du nœud (le plus élevé devient le master).
    advert_int : Intervalle d'annonces VRRP en secondes.
    auth_type : Méthode d'authentification pour VRRP (ici PASS pour un mot de passe simple).
    auth_pass : Le mot de passe partagé.
    virtual_ipaddress : Les adresses IP virtuelles gérées par VRRP.

b. Surveillance de la Santé des Services

Vous pouvez configurer Keepalived pour surveiller des services et basculer l'IP virtuelle si un service échoue.

Exemple : Surveillance d'un Service HTTP

Créez un script de vérification de la santé (par exemple /etc/keepalived/check_http.sh) :

bash

#!/bin/bash

curl -s http://localhost:80 > /dev/null
if [ $? -ne 0 ]; then
  exit 1
else
  exit 0
fi

Rendez le script exécutable :

bash

sudo chmod +x /etc/keepalived/check_http.sh

Mettez à jour la configuration de Keepalived pour utiliser ce script :

bash

global_defs {
   router_id MASTER
}

vrrp_script chk_http {
    script "/etc/keepalived/check_http.sh"
    interval 2
    weight 2
}

vrrp_instance VI_1 {
    state MASTER
    interface eth0
    virtual_router_id 51
    priority 100
    advert_int 1
    authentication {
        auth_type PASS
        auth_pass secret
    }
    virtual_ipaddress {
        192.168.0.100
    }
    track_script {
        chk_http
    }
}

    vrrp_script : Déclare un script de vérification avec son intervalle de vérification.
    track_script : Associe le script de vérification à une instance VRRP.

c. Répartition de Charge avec LVS

Keepalived peut également gérer la répartition de charge avec LVS (Linux Virtual Server).

Exemple : Configuration pour LVS

bash

virtual_server 192.168.0.100 80 {
    delay_loop 10
    lb_algo rr
    lb_kind NAT
    persistence_timeout 50
    protocol TCP

    real_server 192.168.0.101 80 {
        weight 1
        TCP_CHECK {
            connect_timeout 3
        }
    }
    
    real_server 192.168.0.102 80 {
        weight 1
        TCP_CHECK {
            connect_timeout 3
        }
    }
}

    virtual_server : Déclare une IP virtuelle et un port pour le service.
    lb_algo : Algorithme de répartition de charge (rr pour round-robin, wrr pour weighted round-robin, etc.).
    lb_kind : Type de load balancing (NAT, DR, TUN).
    real_server : Les serveurs réels avec leur IP et port.
    TCP_CHECK : Méthode de vérification de la santé des serveurs réels.

3. Démarrer et Activer Keepalived

Sur Debian/Ubuntu :

bash

sudo systemctl start keepalived
sudo systemctl enable keepalived

Sur Red Hat/CentOS :

bash

sudo systemctl start keepalived
sudo systemctl enable keepalived

4. Vérification et Dépannage

    Vérifiez les logs de Keepalived pour des erreurs ou des messages importants :

    bash

sudo tail -f /var/log/syslog | grep keepalived

Utilisez des outils comme ip addr pour vérifier l'assignation des IP virtuelles :

bash

ip addr show
