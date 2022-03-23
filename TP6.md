#  **TP 6 - Services réseau**

## **Exercice : 1**


**Sous-réseau 1 : 172.16.0.64/255.255.255.192**    
* broadcast : 172.16.0.127         
* Première machine : 172.16.0.65  
* Dernière machine : 172.16.0.126 

**Sous-réseau 2 : 172.16.1.64/255.255.255.192**     
* broadcast : 172.16.1.127    
* Première machine : 172.16.1.65  
* Dernière machine : 172.16.1.126  

**Sous-réseau 3 : 172.16.0.0/ 255.255.255.192**     
* broadcast : 172.16.0.63     
* Première machine : 172.16.0.1   
* Dernière machine : 172.16.0.62 

**Sous-réseau 4 : 172.16.0.192/255.255.255.192**    
* broadcast : 172.16.0.255    
* Première machine : 172.16.0.193     
* Dernière machine : 172.16.0.254  

**Sous-réseau 5 : 172.16.1.0/255.255.255.192**   
* broadcast : 172.16.1.63  
* Première machine : 172.16.1.1   
* Dernière machine : 172.16.1.62  

**Sous-réseau 6 : 172.16.0.128/255.255.255.192**     
* broadcast : 172.16.0.191    
* Première machine : 172.16.0.129     
* Dernière machine : 172.16.0.190    

**Sous-réseau 7 : 172.16.1.128/255.255.255.224**    
* broadcast : 172.16.1.159    
* Première machine : 172.16.1.129     
* Dernière machine : 172.16.1.158 


## **Exercice : 2**

## 2.

Pour visualiser les interfaces on utilise la commande : 
```bash
    ip link sh
```
L'interface *lo* correspond à la loopback


## 3.

Pour désinstaller le paquet cloud-init on utilise la commande

```
sudo apt-get purge --auto-remove cloud-init
```

## 4.
Pour renomer la machine on utilise la commande :
```
sudo hostname -b tpadmin.local
```
On modifie ensuite les fichiers /etc/hosts et /etc/hostname avec la commande

```
sudo nano /etc/file
```

## **Exercice : 3**

# 1.

On installe le paquet *isc-dhcp-server* avec la commande :
```
sudo apt install isc-dhcp-server
```

# 2.

Pour attribuer une adresse IP statique de manière permanent, on modifie le fichier */etc/netplan/00-installer-config.yaml*

Pour ajouter une adresse a l'interface choisie. 
 ## 3.

default-lease-time correspond a la durée par default avant expiration de l'adresse ip attribuer.


## 4.

Afin de spécifier l'interface sur laquelle le serveur doit écouter on modifie le fichier */etc/default/isc-dhcp-server* en specifiant *enp0s8* comme interface.

## 5.

On valide la configuration dhcp avec la commande :
```
dhcpd -t
```
Puis on le redémarre avec la commande : 
```
systemctl restart isc-dhcp-server
```

## 7. 

Le client DHCP diffuse un paquet DHCPDISCOVER. Il s’agit d’un message diffusé à l’ensemble des ordinateurs du sous-réseau.

Le serveur DHCP répond en envoyant un paquet DHCPOFFER.

Le client répond à DHCPOFFER en envoyant un DHCPREQUEST.

Le serveur DHCP répond au DHCPREQUEST avec un DHCPACK, ce qui termine le cycle d’initialisation.

## 8.

Le fichier dhcpd.leases est une base de données des concessions du client DHCP.

La commande dhcpd-lease-list affiche les adresse IP attribuées aux machines.

## 10.

## **Exercice : 4**

## 1. 

On décommenter la ligne
*net.ipv4.ip_forward=1* dans le fichier */etc/sysctl.conf* pour autoriser l'IP forwarding. On valide les changements avec la commande :
```
sudo sysctl -p /etc/sysctl.conf
```

## 2.

On autoriser la traduction d’adresse source en ajoutant la règle iptables : 

```
sudo iptables --table nat --append POSTROUTING --out-interface enp0s3 -j MASQUERADE
```

## **Exercice : 5**

## 1.
On installe le paquet bind9 : 
```
sudo apt install bind9
```

## 2.

On modifie le fichier de configuration : */etc/bind/named.conf.options*. On décommente la partie forwarders, et à la place de 0.0.0.0 on renseigne les IP de DNS publics 1.1.1.1 et 8.8.8.8

On redémarre le serveur avec la commande 

```
service named restart
```