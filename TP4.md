#  **TP 4 - Gestion des paquets**



## **Exercice : 1**

## 1. 
    
Pour mettre à jour votre le système on utilise les commandes suivantes :  

```bash
    sudo apt-get update                              
    sudo apt-get upgrade                             
    sudo apt-get dist-upgrade
```

## 2. 

L'*alias* des commandes précédente est le suivant :
```bash
    alias maj='apt-get update && apt-get upgrade && apt-get dist-upgrade'
```


Il faut le mettre dans le fichier .bashrc pour qu'il ne soit pas perdu au prochain démarrage.

## 3.

Pour obtenir les 5 derniers paquets installés ont utilise la commande 
```bash
    cat /var/log/dpkg.log | tail -n 5
```

## 4.

Pour lister les derniers paquets qui ont été installés explicitement avec la commande apt install on utilise la commande :  
```bash
    dpkg -L apt
```

## 5.
Pour compter de deux manières différentes le nombre de total de paquets installés on peut utiliser les commandes suivantes : 
```bash
    apt list --installed | wc -l
    dpkg -l | wc -l
```
La différence est dû aux en-tête des fichiers.  
Le fichier dpkg.log affiche tout l'historique sur les paquets on a donc également les fichiers qui n'ont pas été configuré ou pas été installé entièrement.

## 6. 

Pour savoir combien de paquets sont disponibles en téléchargement sur les dépôts Ubuntu on utilise la commande 
```bash
    apt-cache dumpavail | grep -c \n\n
```

## 7.

Glances est un outil de surveillance du système. 
Hollywood est un programme qui simule un de centre de contrôle affichant des logs qui défilent.


## 8. 

Pour trouver tout les paquets qui proposent de jouer au sudoku on utilise la commande

```bash
    apt search sudoku
```

## **Exercice : 2**

Pour savoir de quel paquet à été installé une commande ont utilise la comande  : 
```bash
    dkpg -S commande
```

```bash
which -a ls | tail -n 1 | xargs dpkg -S | cut -d ":" -f1
```


```bash
#!/bin/bash

origine_commande() {
        paths=$(which -a $1);
        while read -r line; do
                dpkg -S $line > /dev/null 2>&1 ;
                if [ $? = 0 ]; then
                        echo $(dpkg -S $line | cut -d ":" -f1);
                fi
        done <<< "$paths"
}
origine_commande $1
```
On place dans une variable tout les chemins ou se trouyve la commande. On cherche l'emplacement où le paquet est installé si on a pas d'erreur alors on coupe le resultat pour conserver uniquement le nom du paquet qui a installé la commande passer en paramètre.   


## **Exercice : 3**

```bash
#!/bin/bash

is_install() {
        dpkg -l | grep $1 > /dev/null 2>&1
        if [ $? = 0 ]; then
                echo 'INSTALLE';
        else 
                echo 'NON INSTALLE';
        fi
}
is_install $1
```

## **Exercice : 4**

Pour lister les programmes livrés avec coreutils on utilise la commande :
```bash
    dpkg -L coreutils
```
] est la commande test.


## **Exercice : 5**

Emacs est un éditeur de texte très puissant, extensible et personnalisable. 

Lynx est un navigateurs web en mode texte utilisable via une console ou un terminal.
La navigation se fait entièrement au clavier et les différents éléments des pages Web sont mis en évidence grâce à une coloration syntaxique. Il est très populaire en tant que navigateur adapté aux déficiences visuelles car son interface est facile à mettre en œuvre avec un synthétiseur vocal. 


## **Exercice : 6**

Un nouveau fichier a été créé : *linuxuprising-ubuntu-java-impish.list* il contient les informations du dépôts : 
**deb http://ppa.launchpad.net/linuxuprising/java/ubuntu/ impish main**

