# Installation de HAProxy

## Etape 1

Installer le paquet haproxy 
```apt-get update && apt-get install haproxy```

## Etape 2

Configuration exemple : 
```
defaults
    mode http
    timeout client 10s
    timeout connect 5s
    timeout server 10s
    timeout http-request 10s

frontend my_frontend
    bind 127.0.0.1:80
    default_backend first

backend first
    balance roundrobin
    server server1 192.168.50.Y:80
    server server2 192.168.50.Y:80
```

```systemctl restart haproxy```

Source : https://phoenixnap.com/kb/haproxy-load-balancer
