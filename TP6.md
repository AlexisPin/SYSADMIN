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

Pour visualiser lkes interfaces on utilise la commande : 
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

Pour attribuer une adresse IP statique on utilise la commande : 
```
 sudo ip addr add 192.168.100.1/24 dev enp0s8
 ```

 ## 3.

default-lease-time correspond a la durée par default avant expiration de l'adresse ip attribuer.

## 4.
