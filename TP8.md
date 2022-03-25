

Créer user sur les nodes : 
ansible -i inventaire.ini all -m user -a "name=user-ansible password=$6$secretsalt$z4uVW7.aEdFv4Y2ppGBciyk/P8.wyXxldhvki4J5jLeuXaKXBsbVbf04g/2kiQiIHMzWJNzxKEMowOQ0mXKgf group=sudo" -u tp --become --ask-become-pass -ask-pass

