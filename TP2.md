# **TP 2 – Bash**

## Exercice 1 :

### 1. printenv PATH : /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin

### 2. HOME

### 3.

### 4.  MY_VAR=…

### 5. la variable MY_Var n’existe plus après la commande bash

### 6. export MY_VAR=

### 7. export NOM=’prénom nom ’

### 8 . echo "Bonjour à vous, $NOM" ou echo 'Bonjour à vous,' $NOM

### 9. unset supprime la variable, sinon la variable existe toujours mais est vide

### 10.  echo '$HOME=' $HOME


### PATH=$PATH:/chemin par ex $PWD

## Exercice 2 :
 
Contrôle mot de passe :

```bash
#!/bin/bash
testpwd() {
        PASSWORD="azerty"
        read -s -p  'mot de passe :' mdp
        if [ _$mdp == _$PASSWORD ]; then
                echo -e "\nMot de passe corect!"
        else
                echo -e "\nMot de passe incorrect!"
        fi
}
testpwd
```

Calcul factorielle :

```bash
#!/bin/bash
factorielle() {
        local RESULT=1
        if [ $# = 0 ]; then
                echo 'Pas de nombre'
        else
                for i in $(seq 1 $1)
                do
                        ((RESULT=$i*RESULT))
                done
                echo "factorielle $1 est égale à $RESULT"
        fi
}

factorielle $1
```
```bash
#!/bin/bash
statistiques() {
        PARAM_CHECKED=0
        function is_number()
        {
                re='^[+-]?[0-9]+([.][0-9]+)?$'
                if ! [[ $1 =~ $re ]] ; then
                echo 1
                else
                echo 0
                fi
        }
        for param in $* ; do
                if [ $(is_number $param) -eq 1 ]; then
                        echo "Paramètre non valide"
                else
                        PARAM_CHECKED=$(($PARAM_CHECKED + 1))
                fi
        done
        if [ $PARAM_CHECKED == $# ]; then
        tab=()
                for i in $(seq 1 $#); do
                        tab[$i]=$1
                        shift
                done
        echo $tab
        MAX=-100
        MIN=100
        SOMME=0
        for element in $(seq 1 ${#tab[*]}); do
                if [ $element -gt  $MAX ]; then
                        MAX=$element
                elif [ $element -lt $MIN ]; then
                        MIN=$element
                fi
                SOMME= $(($SOMME + $element))
        done
        MOYENNE=$(($SOMME/${#tab[*]}))
        echo "Valeur min : $MIN"
        echo "Valeur max : $MAX"
        echo "Valeur moyenne : $MOYENNE"
        fi
}
statistiques $1 $2 $3
```

```bash
#!/bin/bash
affiche_heure() {
        now=$(date +"%T")
        hour=$(cut -d ':' -f1 <<< $now)
        echo $hour
if [ $(($hour)) -lt 15 ] && [ $(($hour)) -gt 6 ];
then
        echo "$now bonne soirée"
elif [ $(($hour)) -lt 17 ] && [ $(($hour)) -gt 15 ];
then
        echo "$now bonne fin de journée!"
elif [ $(($hour)) -lt 23 ] && [ $(($hour)) -gt 17 ];
then
        echo "$now bonne journée!"
elif [ $(($hour)) -lt 6 ] && [ $(($hour)) -gt 23 ];
then
        echo "$now bonne nuit!"
fi
}
affiche_heure
```