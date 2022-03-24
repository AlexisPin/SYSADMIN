# **TP 3 - Utilisateurs, groupes et permissions Installation de paquets**


useradd -m  -s : création user avec répertoire personnel et bash piur shell

Pour connaître tous les utilisateurs / tous les groupes, il faut regarder la première
colonne des fichiers /etc/passwd / /etc/group

```
cut -d: -f1-4 /etc/passwd
```


forcer un user à changer sont mdp : passwd -e nom_utilisateur

changer mdp : passwd user

se connecter sur user : su user

change groupe d’un fichier/dossier : hgrp [-R] groupe cible


passwd -d :supprimer le mot de passe du compte indiqué

chage user : modifie compte user

chage -l user : informations sur le compte


```
chmod [u g o a] [+ - =] [r w x] nom_du_fichier
```

-chmod u=rx,g=wx,o=r fic = chmod 534 fic
- chmod uo+w,g-rx fic en sachant que les droits initiaux de fic sont r—r-x---  = chmod 602 fic
- chmod 653 fic en sachant que les droits initiaux de fic sont 711  = chmod u=rw, g=rx, o=wx fic
- chmod u+x,g=w,o-r fic en sachant que les droits initiaux de fic sont r—r-x--- = chmod 520 fic


### 2. 
La commande stat permet de récupérer les droits sur un fichier :

```
stat -c %A fichier : classique

stat -c %a fichier : octal
```

#### Umask

Ce masque est une valeur (en octal) qui indique les droits que n’aura pas le
fichier / dossier.

```
$ umask 007
$ umask -S
u=rwx,g=rwx,o=
$ umask g-rw
$ umask -S
u=rwx,g=x,o=
```

#### Sticky bit

Ce t est un bit particulier appelé sticky bit; il indique que dans ce dossier 1
, seuls
le propriétaire d’un fichier, le propriétaire du dossier ou root ont le droit de
renommer ou supprimer ce fichier

```
chmod +t dossier # active le sticky bit
```

Changer le propriétaire-groupe d'un dossier/fichier

```
chown [-R] utilisateur cible
chgrp [-R] groupe cible
```
#### Setuid, Setgid

```
$ stat -c %A /usr/bin/passwd
-rwsr-xr-x
```

Ce s indique que ce programme est exécuté avec les droits de son propriétaire.

```
- chmod 4755 fichier # pour activer le setuid
- chmod 6755 fichier # pour activer les setuid et setgid
```

#### sudo 

La commande sudo mémorise 15 minutes le mot de passe 
La commande sudo -k permet d'oublier le mot de passe 
sudo -i : lance un nouveau shell avec l’environnement de l’utilisateur cible (root)
sudo -s : lance un nouveau shell avec l’environnement de l’utilisateur original

### fichier /etc/shadow

Fichier contenant les mots de passe chiffrés ; 9 champs séparés par ’ :’


### Fichiers /etc/group et /etc/gshadow

Contiennent la liste des utilisateurs appartenant aux différents groupes, et les
mots de passe de groupes.
Format :
- nom du groupe
- champ special
- numero de groupe
- liste des membres 
  
Un utilisateur peut appartenir à plusieurs groupes ; lorsqu’il se connecte, il
appartient au groupe primaire spécifié dans /etc/passwd.

### Gestion des comptes et des mots de passe

- Forcer une utilisateur à changer son mot de passe   
***passwd -e nom_utilisateur***  

- Verrouiller un mot de passe  
***passwd -l nom_utilisateur***   

- Verrouiller un compte : mettre une date d’expiration passée  
 ***usermod --expiredate 0 nom_utilisateur  
 chage --expiredate 0 nom_utilisateur***    

- Réactiver un compte : mettre ”” ou -1   
  ***usermod --expiredate "" nom_utilisateur    
  chage --expiredate -1 nom_utilisateur***
