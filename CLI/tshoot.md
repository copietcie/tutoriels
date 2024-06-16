# I. Linux
* tcpdump
```
tcpdump -nni eth0 net 10.92.0.0/16 and host 10.152.46.124 and 'port 5505 or port 5503' -w DMZ-inbound.pcap

tcpdump -i any -nn host 10.97.40.1 and host 10.155.36.33 and udp port 135

tcpdump -i hn0 -nn host 10.97.40.1 and icmp

```
* nmap
```
nmap -sU -p 123 17.19.48.80 (udp) 
nmap -sT -p 123 17.19.48.80 (tcp) 
nmap -sn 10.131.80.0/24 (discover which hosts are up and running in the 10.131.80.0/24 subnet)
```
Check port open/closed
```
[root@unix01:~]# nmap -Pn 52.214.14.25/32

Starting Nmap 5.51 ( http://nmap.org ) at 2020-05-04 12:53 CEST
Nmap scan report for ec2-52-214-14-25.eu-west-1.compute.amazonaws.com (52.214.14.25)
Host is up (0.024s latency).
Not shown: 997 filtered ports
PORT     STATE  SERVICE
80/tcp   open   http
443/tcp  open   https
3306/tcp closed mysql
```
* ip r g
* netstat
```
[root@linux:~]# netstat -nltup | grep 8080
tcp        0      0 0.0.0.0:8080            0.0.0.0:*               LISTEN      30014/java

[root@debian:~]#  netstat -ntlpu | grep "8080\|8081"

```

# II. pfsense
* Désactiver ou activer toutes les règles de pare-feu
```
pfctl -d
ou
pfctl -e
```
![image](https://github.com/kawaiiineko-website/tutoriels/assets/170332168/ee8ae1a0-188f-4071-89eb-4c408448cdfd)

* En cas de perte de connexion à l'interface graphique après une modification, il est possible de revenir à la sauvegarde dans CLI.
![image](https://github.com/kawaiiineko-website/tutoriels/assets/170332168/7db933a6-e31e-4e0d-b285-c7015b588f6b)

# III. PowerShell
* findstr
```
PS C:\Users\LENOVO> netstat -an | findstr "22"
  TCP    127.0.0.1:62522        0.0.0.0:0              LISTENING
  TCP    172.20.10.14:52420     185.221.85.3:443       ESTABLISHED
  TCP    172.20.10.14:57566     185.221.87.23:443      ESTABLISHED
  TCP    172.20.10.14:58252     140.82.114.22:443      ESTABLISHED
  TCP    172.20.10.14:58464     204.79.197.222:443     ESTABLISHED
```
* pathping --> check source IP/interface
```
PS C:\Users\LENOVO> pathping 192.168.1.1

Tracing route to 192.168.1.1 over a maximum of 30 hops

  0  haivuong-11 [172.20.10.14]
  1  172.20.10.1
  2     *        *        *
```
* route print
```
PS C:\Users\LENOVO> route print
===========================================================================
Interface List
 28...98 fa 9b 88 be 6b ......Realtek PCIe GbE Family Controller
```
