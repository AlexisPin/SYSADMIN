# TP 7 - Boot, services et processus / Tâche               d’administration

## Exercice 1. Personnalisation de GRUB

### 2. 

Pour avoir le menu de GRUB affiché pendant 10s on modifie les lignes 

```
GRUB_TIMEOUT_STYLE=menu  
GRUB_TIMEOUT=10
```
et on laisse la ligne GRUB_DEFAULT=0 

### 3. 

On lance la commande
```
sudo update-grub
```
afin de construire le fichier */boot/grub/grub.cfg* à partir du fichier de paramètre et des scripts.

### 5.

Pour modifier la résolutuon de GRUB on décommente la ligne ci-dessous dans le fihcier  */etc/default/grub* et on choisis la valeur par exemple
```
GRUB_GFXMODE=1280x800
```
### 6. 

Pour modifier le fond d'écran on ajoute la ligne au fichier */etc/default/grub*

```
GRUB_BACKGROUND=/usr/share/images/grub/nom_image
```

### 7.

Pour modifier le thème on installe le paquet *grub2-themes-** et on ajoute la ligne fichier */etc/default/grub*

```
GRUB_THEME=/boot/grub/themes/ubuntustudio/theme.txt
```

### 8.

On ajoute au fichier *40_custom* présent dans le dossier */etc/grub.d* les lignes :

```bash
menuentry "Eteindre" {
halt
}
menuentry "Redémarrer" {
reboot
}
```

### 9. 

Pour modifier la langue du clavier on ajoute la ligne au fichier */etc/default/grub* 

```
GRUB_LANG=fr
```

## Exercice 2. Noyau


### 1. 

On installe le paquet  *build-essential*
```
sudo build-essential
```

### 4. 
Pour compiler le module on utilise la commande *make* et on l'installe avec la commande *make install*


### 5.

Pour charger le module et pour vérifier qu'il a bien été chargé on utilise les commandes
```
insmod hello.ko
lsmod
``` 
On affiche le journal du noyau avec la commande *sudo dmesg* pour vérifier que le module est bien chargé

```
 [Hello world] - La fonction init_module () est appelée .
``` 

### 6. 

Pour obtenir des informations sur le module hello.ko on utilise la commande 

```
modinfo hello.ko 
``` 

On retrouve les informations figurant dans le fichier hello.c transmise dans les macros  *MODULE_XXX*

### 7. 

Pour décharger le module et pour vérifier qu'il a bien été déchargé on utilise les commandes
```
rmmod hello.ko
lsmod
``` 
On lit bien
```
 [Hello world] - La fonction cleanup_module () est appelée .
``` 

dans le journal du noyau.

### 8.

On ajoute dans le fichier */etc/modules* la ligne hello.


## Exercice 3. Interception de signaux

### 1.

```bash
#!/bin/bash

function writter() {
while ( true )
do
        read -p "" ligne;
        echo $ligne >> ./tmp.txt; 
done
}
writter

```

On ligne tout ce que l'on écrit en ligne de commande et l'on redirige le contenu de la ligne dans le fichier tmp.txt. A chaque éxecution la saisie est rajoutée à la fin du fichier.


### 2.

Lorsque l'on appui sur CTRL+Z le processus est mis en pause. Pour poursuivre sont execution on utilise la commande fg

### 3. 

Lorsque l'on appui sur CTRL+C le processus s'arrête.

### 4.
```bash
#!/bin/bash

trap "echo 'Impossible de me placer en arrière-plan' " 20;
trap "echo 'OK, je fais un peu de ménage avant'; rm tmp.txt && killall writter.sh" 2 3;

function writter() {

while ( true )
do
        read -p "" ligne;
        echo $ligne >> ./tmp.txt;
done
}

writter

```

### 5.

On test le script avec les commande clavier et les commandes suivantes 
```
kill -SIGTSTP PID
kill -SIGINT PID
```
### 6.

Pour corriger l'erreur on modifie la ligne suivante 

```bash
trap "echo 'OK, je fais un peu de ménage avant'; test -a tmp.txt && rm tmp.txt; killall writter.sh" 2 3;
```

## Exercice 4. Surveillance de l’activité du système

### 1.
